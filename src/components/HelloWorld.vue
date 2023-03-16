<template>
  <div class="draggable " :style="{ left: position.x + 'px', top: position.y + 'px' }" @mousedown="startDrag" :class="checkTransaction">
    Drag me!
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDragging: false,
      startPosition: { x: 0, y: 0 },
      position: { x: 0, y: 0 },
      checkTransaction: "",
    };
  },
  methods: {
    startDrag(event) {
      this.checkTransaction = "";
      this.isDragging = true;
      this.startPosition.x = event.clientX;
      this.startPosition.y = event.clientY;
      // this.position.x = event.clientX;
      // this.position.y = event.clientY;
      window.addEventListener("mousemove", this.drag);
      window.addEventListener("mouseup", this.stopDrag);
    },
    drag(event) {
      if (this.isDragging) {
        const deltaX = event.clientX - this.startPosition.x;
        const deltaY = event.clientY - this.startPosition.y;
        this.position.x += deltaX;
        this.position.y += deltaY;
        this.startPosition.x = event.clientX;
        this.startPosition.y = event.clientY;
      }
    },
    stopDrag() {
      this.isDragging = false;
      this.checkTransaction = "trans-css"
      if(this.position.y < window.innerHeight * 0.2 ){
        this.position.y = 0;
      }else if(this.position.y  > window.innerHeight * 0.8){
        this.position.y = window.innerHeight - 100;
      }else if(this.position.x < window.innerWidth /2){
        this.position.x = 0;
      }else{
        this.position.x = window.innerWidth - 100;
      }

      if(this.position.x < 0){
        this.position.x = 0;
      }

      if(this.position.x > window.innerWidth-100){
        this.position.x = window.innerWidth - 150
      }

      console.log(this.position.y);
      window.removeEventListener("mousemove", this.drag);
      window.removeEventListener("mouseup", this.stopDrag);
    }
  }
};
</script>

<style>
.draggable {
  position: absolute;
  width: 100px;
  height: 100px;
  background-color: blue;
  color: white;
  text-align: center;
  user-select: none;
  cursor: grab;

}

.trans-css{
  transition: 0.5s;
}
</style>