<template>
 <div class="canvas">
    <div
      class="box"
      v-for="(box, index) in boxes"
      :key="index"
      @click="toggleBox(index)"
      :style="{ 'background-color': box.selected ? 'rgba(0, 0, 255, 0.5)' : '' }"
    ></div>
 </div>
</template>

<script>
export default {
 data() {
    return {
      boxes: Array(1024).fill({ selected: false }),
    };
 },
 methods: {
  toggleBox(index) {
    if (this.boxes[index].selected) {
      this.boxes = this.boxes.map((box) => ({ ...box, selected: false }));
    } else {
      this.boxes[index].selected = true;
    }


    if (window.innerWidth < 768) {
      const randomIndex = Math.floor(Math.random() * this.boxes.length);
      this.boxes[randomIndex].selected = true;
    }
  },
 },
};
</script>

<style scoped>
body {
 background-color: #121212;
 background-image: radial-gradient(circle at 32px 32px, black 1px, transparent 0);
 background-size: 32px 32px;
 box-sizing: border-box;
}
.canvas {
  display: grid;
  grid-template-columns: repeat(32, 1fr);
  grid-template-rows: repeat(32, 1fr);
  width: 3200px;
  height: 3200px;
  /* border: 1px dotted; */
}

.box {
 position: relative;
 width: 100px;
 height: 100px;
 background-color: #212121;
 box-sizing: border-box;
 /* border: 1px solid #f5f5f5; */
}
.box {
  border: 1px solid #313131;
  width: 100px;
  height: 100px;
  position: relative;
}

.box::before,
.box::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 50%;
  height: 50%;
  background-color: rgba(0, 0, 255, 0.5);
  transform: translate(-50%, -50%);
  opacity: 0;
  transition: opacity 0.2s ease-in-out;
}

.box::before {
  border-top: 1px solid #f5f5f5;
  border-left: 1px solid #f5f5f5;
}

.box::after {
  border-bottom: 1px solid #f5f5f5;
  border-right: 1px solid #f5f5f5;
}

.box:hover::before,
.box:hover::after {
  opacity: 1;
}

.box:hover {
 background-color: #313131;
 cursor: pointer;
}
</style>