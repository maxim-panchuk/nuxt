<script setup lang="ts">
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
        const url = 'https://9dea-88-201-232-88.ngrok-free.app/check-wallet';
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
            console.log(JSON.stringify(data))
            if (data.walletExists) {
                walletAddress.value = data.address;
                walletBalance.value = data.balance;
                walletStatus.value = 'Кошелек найден';
            } else {
                walletStatus.value = 'Кошелька нет!';
            }
        } else {
            showAlert('Ошибка при проверке кошелька');
        }
    } catch (err) {
        showAlert(`Ошибка запроса: ${err}`);
    }
}

async function createWallet() {
    try {
        const url = 'https://9dea-88-201-232-88.ngrok-free.app/wallet';
        const resp = await fetch(url, {
            method: 'POST',
            headers: {
                'ngrok-skip-browser-warning': '1',
                'Content-Type': 'text/plain',
            },
            body: initData, // Отправляем initData для создания кошелька
        });
        if (resp.ok) {
            showAlert('Кошелек успешно создан');
            // Повторно проверяем кошелек после создания
            checkWallet();
        } else {
            showAlert('Ошибка при создании кошелька');
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

        <p>{{ walletStatus }}</p>

        <div v-if="walletAddress">
            <p>Адрес кошелька: {{ walletAddress }}</p>
            <p>Баланс: {{ walletBalance }} TON</p>
        </div>

        <div v-else>
            <p>Для создания кошелька нажмите на кнопку ниже</p>
        </div>

        <MainButton text="Создать кошелек" @click="createWallet" />
    </section>
</template>