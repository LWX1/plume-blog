<template>
    <!-- <canvas id="myCanvas"></canvas> -->
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { startCanvas } from '../public/js/ball.js';
const ctx = ref("");

const getCanvas = () => {
    let canvas = document.getElementById('canvas');
    canvas.width = document.documentElement.clientWidth;
    canvas.height = document.documentElement.clientHeight;
    this.ctx = canvas.getContext('2d');
}

onMounted(() => {
    ctx.value = startCanvas({
        dom: '', // 没有默认为dom
        number: 200
    })
})

onUnmounted(() => {
    ctx.value.clearRect();
})




</script>

<style></style>