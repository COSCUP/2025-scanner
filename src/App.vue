<script setup lang="ts">
import { ref } from 'vue'
import { QrcodeStream } from 'vue-qrcode-reader'
import { useToast } from 'vue-toastification'

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
  <div>
    <h1>QR Code Scanner</h1>
    <qrcode-stream @detect="onDetect"></qrcode-stream>
    
  </div>
</template>

<style scoped>
</style>