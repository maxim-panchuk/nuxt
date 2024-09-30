<!-- ProfilePage.vue -->
<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
const { showAlert } = await import('vue-tg').then(mod => mod.useWebAppPopup());
const { initData } = await import('vue-tg').then(mod => mod.useWebApp());

const walletAddress = ref<string | null>(null);
const walletBalance = ref<number | null>(null);
const walletStatus = ref<string>('Checking wallet...');
const router = useRouter();

async function checkWallet() {
  try {
    const url = 'https://m2y5ao-88-201-232-88.ru.tuna.am/check-wallet';
    const resp = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'text/plain',
      },
      body: initData,
    });
    if (resp.ok) {
      const data = await resp.json();
      walletAddress.value = data.address;
      walletBalance.value = data.balance;
      walletStatus.value = 'Wallet found';
    } else {
      showAlert('Error checking wallet');
    }
  } catch (err) {
    showAlert(`Request error: ${err}`);
  }
}

onMounted(() => {
  checkWallet();
});

function navigateToTopUp() {
  console.log(walletAddress.value)
  router.push({ name: 'TopUpPage', state: { walletAddress: walletAddress.value} });
}
</script>

<template>
  <section class="wallet-container">
    <div class="wallet-info">
      <p class="balance-text">{{ walletBalance !== null ? `${walletBalance} TON` : walletStatus }}</p>
    </div>
    <button class="top-up-button" @click="navigateToTopUp">Top up</button>
  </section>
</template>

<style scoped>
.wallet-container {
  background-color: #1C1C1E; /* Темный фон */
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.wallet-info {
  margin-bottom: 20px;
}

.balance-text {
  color: white; /* Белый текст */
  font-size: 48px; /* Крупный шрифт для баланса */
  font-weight: bold;
  font-family: 'SF Pro Display', sans-serif; /* Шрифт как в Telegram */
}

.top-up-button {
  background-color: #007AFF; /* Синий цвет кнопки */
  color: white; /* Белый цвет текста на кнопке */
  border: none;
  border-radius: 12px;
  padding: 15px 30px;
  font-size: 18px;
  font-family: 'SF Pro Display', sans-serif;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.top-up-button:hover {
  background-color: #005BBB; /* Темнее при наведении */
}
</style>
