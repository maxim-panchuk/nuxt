<script lang="ts" setup>

import { ref, onMounted } from 'vue';
const { MainButton, useWebAppPopup, useWebApp } = await import('vue-tg');
const { showAlert } = useWebAppPopup();
const { initData } = useWebApp();


const walletAddress = ref<string | null>(null);
const walletBalance = ref<number | null>(null);
const walletStatus = ref<string>('Проверяем наличие кошелька...');


async function checkWallet() {
    try {
        console.log(initData)
        const url = 'https://da2f-88-201-232-88.ngrok-free.app/check-wallet';
        const resp = await fetch(url, {
            method: 'POST',
            headers: {
                'ngrok-skip-browser-warning': '1',
                'Content-Type': 'text/plain',
            },
            body: initData,
        });
        if (resp.ok) {
            const data = await resp.json();
            console.log(data)
            walletAddress.value = data.address;
            walletBalance.value = data.balance
            walletStatus.value = 'Кошелек найден';
        } else {
            showAlert('Ошибка при проверке кошелька');
        }
    } catch (err) {
        showAlert(`Ошибка запроса: ${err}`);
    }
}


onMounted(() => {
    checkWallet();
});
</script>

<template>
  <section>
    <h1>Информация о кошельке</h1>
    <div>
        <p>Адрес кошелька: {{ walletAddress }}</p>
        <p>Баланс: {{ walletBalance }}</p>
    </div>
  </section>
</template>

<style>

</style>