<!-- TopUpPage.vue -->
<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import { useRouter, useRoute } from 'vue-router';
const { showAlert } = await import('vue-tg').then(mod => mod.useWebAppPopup());

//const walletAddress = ref<string>('EQC2D7...fFP0Zl'); // Пример адреса
const router = useRouter();
const walletAddress = ref<string | null>(null);

onMounted(() => {
  const state = history.state;
  if (state && state.walletAddress) {
    walletAddress.value = state.walletAddress;
  } else {
    walletAddress.value = 'wallet not found'
  }
});

function copyAddress() {
  if (walletAddress.value) {
    navigator.clipboard.writeText(walletAddress.value);
    showAlert('Address copied to clipboard!');
  }
}
function goBack() {
  router.back();
}
</script>

<template>
  <section class="top-up-container">
    <button class="back-button" @click="goBack">← Back</button>
    <div class="text-section">
      <p class="lorem-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </div>
    <div class="address-section">
      <p class="wallet-address">Address: {{ walletAddress }}</p>
      <button class="copy-button" @click="copyAddress">Copy address</button>
    </div>
  </section>
</template>

<style scoped>
.top-up-container {
  background-color: #1C1C1E; /* Темный фон */
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.back-button {
  align-self: flex-start;
  background-color: transparent;
  color: #007AFF; /* Синий цвет текста */
  border: none;
  font-size: 18px;
  font-family: 'SF Pro Display', sans-serif;
  cursor: pointer;
  margin-bottom: 20px;
}

.text-section {
  margin-bottom: 20px;
  text-align: center;
}

.lorem-text {
  color: white; /* Белый текст */
  font-size: 16px;
  font-family: 'SF Pro Display', sans-serif;
}

.address-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.wallet-address {
  color: white; /* Белый текст */
  font-size: 18px;
  font-family: 'SF Pro Display', sans-serif;
}

.copy-button {
  background-color: #007AFF; /* Синий цвет кнопки */
  color: white; /* Белый цвет текста на кнопке */
  border: none;
  border-radius: 12px;
  padding: 10px 20px;
  font-size: 16px;
  font-family: 'SF Pro Display', sans-serif;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.copy-button:hover {
  background-color: #005BBB; /* Темнее при наведении */
}
</style>
