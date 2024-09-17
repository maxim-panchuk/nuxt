<template>
    <div>
      <!-- Кнопка для открытия модального окна -->
      <button @click="openModal" class="open-button">Connect your wallet</button>
  
      <!-- Модальное окно -->
      <div v-if="isModalVisible" class="modal-backdrop" @click="closeModal">
        <div class="modal-content" @click.stop>
          <!-- Кнопка закрытия -->
          <button class="close-button" @click="closeModal">✕</button>
  
          <!-- Заголовок и подзаголовок -->
          <div class="modal-header">
            <h2>Connect your wallet</h2>
            <p>Open Wallet in Telegram or select your wallet to connect</p>
          </div>
  
          <!-- Кнопка для открытия кошелька в Telegram -->
          <button class="telegram-button" @click="showAlert('Telegram Wallet')">
            <img src="https://upload.wikimedia.org/wikipedia/commons/8/82/Telegram_logo.svg" alt="Telegram" />
            Open Wallet in Telegram
          </button>
  
          <!-- Список кошельков с горизонтальной прокруткой -->
          <div class="wallet-list">
            <button @click="showAlert('Tonkeeper')">
              <img src="https://tonkeeper.com/assets/images/favicon.png" alt="Tonkeeper" />
              Tonkeeper
            </button>
            <button @click="showAlert('MyTonWallet')">
              <img src="https://mytonwallet.org/assets/logo.png" alt="MyTonWallet" />
              MyTonWallet
            </button>
            <button @click="showAlert('Tonhub')">
              <img src="https://tonhub.com/favicon.ico" alt="Tonhub" />
              Tonhub
            </button>
            <button @click="showAlert('DeWallet')">
              <img src="https://dewallet.app/favicon.ico" alt="DeWallet" />
              DeWallet
            </button>
            <button @click="showAlert('BitgetTonWallet')">
              <img src="https://example.com/bitget.png" alt="BitgetTonWallet" />
              BitgetTonWallet
            </button>
            <button @click="showAlert('SafePalWallet')">
              <img src="https://example.com/safepal.png" alt="SafePalWallet" />
              SafePalWallet
            </button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  // Состояние для видимости модального окна
  const isModalVisible = ref(false);
  
  // Открыть модальное окно
  function openModal() {
    isModalVisible.value = true;
  }
  
  // Закрыть модальное окно
  function closeModal() {
    isModalVisible.value = false;
  }
  
  // Вызов алерта при выборе кошелька
  function showAlert(walletName) {
    alert(`Selected: ${walletName}`);
  }
  </script>
  
  <style scoped>
  /* Основные стили для шрифтов и кнопок */
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
  
  * {
    font-family: 'Roboto', sans-serif;
  }
  
  .open-button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #007AFF;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-content {
    background-color: #1C1C1E;
    width: 90%;
    max-width: 500px;
    border-radius: 20px;
    padding: 20px;
    position: relative;
    color: white;
  }
  
  /* Кнопка закрытия */
  .close-button {
    position: absolute;
    top: 10px;
    left: 10px;
    background: none;
    border: none;
    font-size: 24px;
    color: white;
    cursor: pointer;
  }
  
  /* Заголовок и подзаголовок */
  .modal-header h2 {
    font-size: 24px;
    margin-bottom: 5px;
  }
  
  .modal-header p {
    font-size: 14px;
    color: #A8A8A8;
  }
  
  /* Кнопка для открытия кошелька в Telegram */
  .telegram-button {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    background-color: #007AFF;
    color: white;
    padding: 15px;
    border-radius: 10px;
    margin: 20px 0;
    font-size: 18px;
    border: none;
    cursor: pointer;
  }
  
  .telegram-button img {
    margin-right: 10px;
    width: 24px;
    height: 24px;
  }
  
  /* Горизонтальный список кошельков */
  .wallet-list {
    display: flex;
    gap: 15px;
    overflow-x: auto;
    padding: 10px 0;
  }
  
  .wallet-list button {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: none;
    border: none;
    color: white;
    cursor: pointer;
    min-width: 80px;
    text-align: center;
  }
  
  .wallet-list img {
    width: 32px;
    height: 32px;
    margin-bottom: 5px;
  }
  </style>
  