<template>
    <div>
      <canvas ref="secondCanvas" class="secondcanvas"></canvas>
    </div>
  </template>
  
  <script>
//   import { ref, onMounted } from 'vue';
  import { fabric } from 'fabric';
  
  export default {
    name: 'SecondCanvas',
  mounted() {
    this.canvas = new fabric.Canvas(this.$refs.canvas);
    this.canvas.setDimensions({width:500, height:500});
    this.canvas.on('object:moving', this.handleObjectMoving);
  },
  methods: {
    handleObjectMoving(event) {
      const selectedObjects = this.canvas.getActiveObjects();
      if (selectedObjects.length > 1) {
        const group = new fabric.Group(selectedObjects, {
          left: event.target.left,
          top: event.target.top,
        });
        this.canvas.add(group);
        this.canvas.discardActiveObject();
      }
    },
  },
  };
  </script>

<style scoped>
.secondcanvas {
    background-color: rgb(56, 56, 56);
}
</style>
  