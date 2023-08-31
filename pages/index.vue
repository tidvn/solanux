<template>
  <ClientOnly>
    <div>
      <WalletMultiButton />
      <p>{{ $wallet.publicKey.value?.toBase58() ?? "Not connected" }}</p>
      <button @click="fetchBalance"> fetchBalance</button>
      <p>{{ balance }}</p>
    </div>
  </ClientOnly>
</template>

<script setup>
import { ref } from 'vue';
import { useAnchorWallet , WalletMultiButton,useWallet } from 'solana-wallets-vue';
import { Connection, clusterApiUrl } from '@solana/web3.js';
useAnchorWallet()
const { publicKey, connected } = useWallet();

console.log(useWallet())
const balance = ref(0);
const fetchBalance = async () => {
    const connection = new Connection(clusterApiUrl('devnet'));
    const balanceValue = await connection.getBalance(publicKey.value) || 0;
    balance.value = balanceValue ;    
};

</script>
