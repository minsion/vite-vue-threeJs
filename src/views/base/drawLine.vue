<template>
  <div id="three-dom" ref="screenDom"></div>
</template>
<script setup>
import * as THREE from 'three'
import { onMounted, ref } from 'vue';

const screenDom = ref(null)
const scene = new THREE.Scene()

onMounted(() => {
  init()
})
const init = () => {
  // 透视摄像机
  const camera = new THREE.PerspectiveCamera(45, screenDom.value.clientWidth / screenDom.value.clientHeight, 0.1, 1000)
  camera.position.set(0, 0, 100);
  camera.lookAt(0, 0, 0);

  const renderer = new THREE.WebGLRenderer()
  renderer.setSize(screenDom.value.clientWidth, screenDom.value.clientHeight)
  screenDom.value.appendChild(renderer.domElement)
  const material = new THREE.LineBasicMaterial({
    color: 0x00ff00
  })
  const points = [];
  points.push(new THREE.Vector3(- 10, 0, 0));
  points.push(new THREE.Vector3(0, 10, 0));
  points.push(new THREE.Vector3(10, 0, 0));

  const geometry = new THREE.BufferGeometry().setFromPoints(points)

  const line = new THREE.Line(geometry, material)
  scene.add(line)
  renderer.render(scene, camera)
}

</script>
<style lang="less" scoped>
#three-dom {
  width: 100%;
  height: 100%;
}
</style>