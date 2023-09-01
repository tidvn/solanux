<script lang="ts">
import { WalletMultiButton } from 'solana-wallets-vue';
export default {
  emits: ['topbar-menu-toggle', 'menu-toggle'],
  computed: {
    darkTheme() {
      return this.$appState.darkTheme;
    }
  },
  methods: {
    onMenuToggle(event: any) {
      this.$emit('menu-toggle', event);
    },
    onTopbarMenuToggle(event: any) {
      this.$emit('topbar-menu-toggle', event);
    },
    topbarImage() {
      return this.$appState.darkTheme ? '/images/logo-white.svg' : '/images/logo-dark.svg';
    }
  },
  components:{
    WalletMultiButton,
  }
};
</script>

<template>
  <div class="layout-topbar">
    <NuxtLink to="/" class="layout-topbar-logo">
      <img alt="Logo" :src="topbarImage()">
      <span>Tidvn</span>
    </NuxtLink>
    <button class="p-link layout-menu-button layout-topbar-button" @click="onMenuToggle">
      <i class="pi pi-bars" />
    </button>

    <button
      v-styleclass="{
        selector: '@next',
        enterClass: 'hidden',
        enterActiveClass: 'scalein',
        leaveToClass: 'hidden',
        leaveActiveClass: 'fadeout',
        hideOnOutsideClick: true
      }"
      class="p-link layout-topbar-menu-button layout-topbar-button"
    >
      <i class="pi pi-ellipsis-v" />
    </button>
    <ul class="layout-topbar-menu hidden lg:flex origin-top"> 
      <ClientOnly>
        <WalletMultiButton />
      </ClientOnly>   
      
    </ul>
  </div>
</template>
