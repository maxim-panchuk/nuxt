<script>
import { TonConnectUIProvider, TonConnectButton } from '@townsquarelabs/ui-vue';

export default {
  components: {
    TonConnectUIProvider,
    TonConnectButton,
  },
  setup(){
    const options = {
      manifestUrl:"https://<YOUR_APP_URL>/tonconnect-manifest.json",
    };
    return {
      options
    }
  }
}
</script>

<template>
    <section>
        <NuxtLink to="/profile">Профиль</NuxtLink>
        <TonConnectUIProvider :options="options">
            <TonConnectButton />
        </TonConnectUIProvider>
    </section>
</template>