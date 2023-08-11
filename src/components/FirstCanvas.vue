<template>
  <div id="first">
    <span>Canvas 1</span>
    <canvas ref="firstCanvas" class="firstcanvas"></canvas>
  </div>
  <div id="second">
    <span>Canvas 2</span>
    <canvas ref="secondCanvas" class="secondcanvas"></canvas>
  </div>
</template>
  
  <script>
import { ref, onMounted } from "vue";
import { fabric } from "fabric";
import axios from "axios";

export default {
  name: "FirstCanvas",
  setup() {
    const firstCanvas = ref(null);
    const secondCanvas = ref(null);
    let selectedImage = null;

    onMounted(() => {
      const canvas1 = new fabric.Canvas(firstCanvas.value);
      canvas1.setDimensions({ width: 650, height: 500 });

      const canvas2 = new fabric.Canvas(secondCanvas.value);
      canvas2.setDimensions({ width: 650, height: 500 });
      axios
        .get("https://jsonplaceholder.typicode.com/photos")
        .then((response) => {
          const images = response.data
            .filter((image) => image.id % 2 === 0)
            .slice(-10);

          images.forEach((image, index) => {
            // images.forEach((image, index) => {
            
            fabric.Image.fromURL(image.thumbnailUrl, function (img) {
              canvas1.add(
                img.set({
                  left: index * 80,
                  top: 10,
                  width: 70,
                  height: 70,
                  originX: "left",
                  originY: "top",
                  selectable: true
                })
              );
            });
          });
        });

      canvas1.on("mouse:down", (event) => {
        selectedImage = event.target;
        console.log(selectedImage);
      });

      //Handle image dropping on target canvas
      canvas2.on("mouse:up", (event) => {
        if (selectedImage) {
          //   const clonedImage = selectedImage.clone();
          const clonedImage = selectedImage;
          console.log(clonedImage);
          clonedImage.set({ left: event.pointer.x, top: event.pointer.y });
          canvas1.remove(selectedImage);
          canvas2.add(clonedImage);
          selectedImage = null;
        }
      });
    });

    return {
      firstCanvas,
      secondCanvas,
    };
  },
};
</script>

  <style scoped>
.firstcanvas {
  border-style: solid;
  border-color: black;
  flex: 1;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.secondcanvas {
  border-style: solid;
  border-color: black;
}

#first {
  float: left;
}
#second {
  float: right;
}
</style>
  