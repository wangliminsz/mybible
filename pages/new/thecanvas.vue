<template>
  <div class="flex">
    <!-- <div class="m-3 flex-none">
      <button
        class="px-3 py-1 bg-blue-500 border rounded shadow-2xl text-white text-sm flex-none"
      >
        OK Confirm
      </button>
    </div> -->

    <canvas id="canvas"></canvas>

    <button onclick="canvasText()" class="text:black">Hello Canvas</button>
    
  </div>
    
</template>

<script>
export default {

   head: {
    script: [
      {
        src: "/js/myCanvas.js",
      },
    ],
  },


};
</script>

<style>
</style>