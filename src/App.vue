<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { QrcodeStream } from 'vue-qrcode-reader'
import { useToast } from 'vue-toastification'
import coscupLogo from './assets/coscup.svg'

const decodedString = ref('')
const token = ref<string | null>(null)
const toast = useToast()

onMounted(() => {
  const urlParams = new URLSearchParams(window.location.search)
  const tokenFromUrl = urlParams.get('token')
  if (tokenFromUrl) {
    token.value = tokenFromUrl
  }
})

function onDetect(detectedCodes: any[]) {
  const result = detectedCodes[0].rawValue
  decodedString.value = result
  console.log(result)
  toast.warning("公尚未開放！", {
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
