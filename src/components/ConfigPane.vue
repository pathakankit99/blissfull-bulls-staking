<template>
<div v-if="!nameOfWallet" class="center mb-6">
<button class="nes-btn is-primary" @click="connectToWallet">Connect Wallet</button>
</div>
<div v-else class="center mb-6">
<button class="nes-btn is-primary" @click="connectToWallet">Connected</button>
</div>
  <div class="flex hidden justify-center mb-10">
    <div class="nes-select is-dark flex-1">
      <select required id="cluster" v-model="chosenCluster">
        <option :value="Cluster.Mainnet">Mainnet</option>
        <option :value="Cluster.Devnet">Devnet</option>
        <option :value="Cluster.Testnet">Testnet</option>
        <option :value="Cluster.Localnet">Localnet</option>
      </select>
    </div>
    <div class="nes-select is-dark flex-1">
      <select required id="wallet" v-model="chosenWallet">
        <option :value="WalletName.Phantom">Phantom</option>
      </select>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue';
import { WalletName } from '@solana/wallet-adapter-wallets';
import useCluster, { Cluster } from '@/composables/cluster';
import useWallet from '@/composables/wallet';

export default defineComponent({
  setup() {
    // cluster
    const { cluster, setCluster, getClusterURL } = useCluster();
    const chosenCluster = computed({
      get() {
        return cluster.value;
      },
      set(newVal: Cluster) {
        setCluster(newVal);
      },
    });

    // wallet
  
    const { getWalletName, setWallet } = useWallet();
    const chosenWallet = computed({
      get() {
        return getWalletName();
      },
      set(newVal: WalletName | null) {
        setWallet("Phantom", getClusterURL());
      },
    });
     const connectToWallet=()=>{
       setWallet("Phantom", getClusterURL())
     }
     
      const nameOfWallet = computed({
        get(){
          return getWalletName();
        },
        set(){
          return null;
        }
      })

     console.log(nameOfWallet,'walletName')
    return {
      Cluster,
      chosenCluster,
      WalletName,
      chosenWallet,
      connectToWallet,
      nameOfWallet
    };
  },
});
</script>

<style scoped></style>
