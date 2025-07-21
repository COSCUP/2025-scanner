<script setup lang="ts">
import { ref } from 'vue'
import { QrcodeStream } from 'vue-qrcode-reader'
import { useToast } from 'vue-toastification'
import coscupLogo from './assets/coscup.svg'

const decodedString = ref('')
const toast = useToast()

function onDetect(detectedCodes: any[]) {
  const result = detectedCodes[0].rawValue
  decodedString.value = result
  console.log(result)
  toast.success("掃描成功！", {
    position: "bottom-center",
    timeout: 3000,
  })
}
</script>

<template>
  <div class="main-container">
    <img :src="coscupLogo" alt="COSCUP Logo" class="logo" />
    <div class="scanner-container">
      <qrcode-stream @detect="onDetect"></qrcode-stream>
    </div>
  </div>
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
}
</style>

<style scoped>
.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  gap: 2rem;
}

.logo {
  width: 250px;
}

.scanner-container {
  width: 80vw;
  max-width: 600px;
  height: 80vw;
  max-height: 600px;
  border: 1px solid #ccc;
}
</style>