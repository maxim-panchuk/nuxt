<script setup lang="ts">
const { MainButton, useWebAppPopup, useWebApp } = await import('vue-tg')
const { showAlert } = useWebAppPopup();
const { initData } = useWebApp();
async function createWallet() {
    try {
        console.log(initData)
        const url = 'https://9aee-88-201-232-88.ngrok-free.app/wallet';
        const resp = await fetch(url, {
            method: 'POST',
            headers: {
                'ngrok-skip-browser-warning': '1',
                'Content-Type': 'text/plain',
            },
            body: initData,
        });
        if (resp.ok) {
            const data = await resp.text();
            showAlert(`Sucesss`)
        } else {
            showAlert(`Error`)
        }
    } catch(err) {
        showAlert(`Request failed: ${err}`)
    }
}
</script>

<template>
    <section>
        <h1>Hello Telegram Mini App</h1>
        <MainButton text='get message' @click="createWallet"/>
    </section>
</template>