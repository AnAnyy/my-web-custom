<script setup>
import { onMounted, ref,onBeforeUnmount } from "vue";

defineProps({
  msg: String,
});
const count = ref(0);

onMounted(() => {
  // 监听来自Flutter的消息
  window.addEventListener("updateVueData", updateData);
});

onBeforeUnmount(() => {
  // 监听来自Flutter的消息
  window.removeEventListener("updateVueData", updateData);
});

function updateData(data) {
  count.value = data.detail;
}
function sendToFlutter() {
  window.flutterBridge.postMessage("Hello from JavaScript!");
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
  </div>
  <button @click="sendToFlutter()">
    Send Message to Flutter And Get Flutter Data
  </button>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
