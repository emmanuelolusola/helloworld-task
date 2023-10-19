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
      this.boxes = this.boxes.map((box) => ({ ...box, selected: false }));

      this.boxes[index].selected = true;
    },
 },
};
</script>

<style scoped>
body {
 background-color: #121212;
 color: #f5f5f5;
 box-sizing: border-box;
}
.canvas {
 display: grid;
 grid-template-columns: repeat(32, 1fr);
 grid-template-rows: repeat(32, 1fr);
 width: 3200px;
 height: 3200px;
}

.box {
 position: relative;
 width: 100px;
 height: 100px;
 background-color: #212121;
 box-sizing: border-box;
}

.box::before,
.box::after {
 content: "";
 position: absolute;
 width: 6px;
 height: 6px;
 background-color: #f5f5f5;
 border-radius: 50%;
 margin-left: -2px;
 margin-top: -2px;
}

.box:hover {
 background-color: #313131;
}
</style>