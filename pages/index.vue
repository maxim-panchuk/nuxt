<template>
    <div>
      <!-- Кнопка для открытия модального окна -->
      <button @click="openModal" class="open-button">Connect your wallet</button>
      <!-- Модальное окно -->
      <div v-if="isModalVisible" class="modal-backdrop" @click="closeModal">
        <div class="modal-content" @click.stop>
          <!-- Текст "Закрыть" вместо кнопки закрытия с небольшим отступом -->
          <button class="close-text" @click="closeModal">Закрыть</button>
  
          <!-- Заголовок и подзаголовок -->
          <div class="modal-header">
            <h2>Connect your wallet</h2>
            <p>Open Wallet in Telegram or select your wallet to connect</p>
          </div>
  
          <!-- Кнопка для открытия кошелька в Telegram -->
          <button class="telegram-button" @click="connectTelegramWallet">
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
  import { TonConnectUI } from '@tonconnect/ui'
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

  async function connectTelegramWallet() {
    try {
      const url = 'https://m2y5ao-88-201-232-88.ru.tuna.am/connect-wallet'
      const resp = await fetch(url, {
        method: 'POST',
        headers: {
          'Content-Type': 'text/plain',
        },
      });
      if (resp.ok) {
        const data = await resp.text();
        showAlert(data)
      }
    } catch (err) {
      showAlert(`Request error: ${err}`)
    }
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
    align-items: flex-end; /* Всплывание снизу */
    justify-content: center;
  }
  
  .modal-content {
    background-color: #1C1C1E;
    width: 100%;
    max-width: 500px;
    height: auto; /* Автоматическая высота */
    border-radius: 20px 20px 0 0;
    padding: 20px;
    position: relative;
    color: white;
    animation: slide-up 0.3s ease;
  }
  
  /* Анимация для появления окна снизу */
  @keyframes slide-up {
    from {
      transform: translateY(100%);
    }
    to {
      transform: translateY(0);
    }
  }
  
  /* Кнопка "Закрыть" */
  .close-text {
    position: absolute;
    top: 10px;
    left: 20px; /* Добавлен отступ слева */
    background: none;
    border: none;
    font-size: 14px;
    color: #007AFF; /* Синий цвет в стиле Telegram */
    cursor: pointer;
    text-transform: none; /* Сделано с маленькой буквы */
  }
  
  /* Заголовок и подзаголовок */
  .modal-header {
    text-align: center; /* Выровнять текст по центру */
  }
  
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
    width: 80%; /* Уменьшение ширины кнопки */
    background-color: #007AFF;
    color: white;
    padding: 12px; /* Уменьшение padding */
    border-radius: 10px;
    margin: 20px auto; /* Центрирование кнопки */
    font-size: 16px; /* Уменьшение шрифта */
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
    justify-content: center;
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
  