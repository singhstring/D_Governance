<template>
  <v-app>
  <img src="dl.png" alt="">
    <v-toolbar flat dark color="#1B5E20">
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <main>
      <v-alert error value="true" v-if="!metamask">
        This application requires the MetaMask Chrome Plugin
      </v-alert>
      <template v-if="metamask">
        <v-container>
          <v-layout row class="pb-5">
            <wallet-info></wallet-info>
            <send-tokens></send-tokens>
          </v-layout>

          <v-layout row class="pb-5">
            <blkd></blkd>
            <send-message></send-message>
          </v-layout>

          <v-layout row class="pb-5">
            <transactions></transactions>
          </v-layout>

          <v-layout row class="pb-5">
            <chats></chats>
          </v-layout>

        </v-container>
      </template>
    </main>
    <v-footer fixed>
      <span>&copy; 2018</span>
    </v-footer>
  </v-app>
</template>

<script>

import WalletInfo from './components/WalletInfo.vue'
import SendTokens from './components/SendTokens.vue'
import Blkd from './components/Blkd.vue'
import SendMessage from './components/SendMessage.vue'
import Transactions from './components/Transactions.vue'
import Chats from './components/Chats.vue'





export default {

  components: {
    WalletInfo,
    SendTokens,
    Blkd,
    SendMessage,
    Transactions,
    Chats
  },

  data () {
    return {
      title: 'D GOVERNANCE'
    }
  },

  computed: {
    metamask () {
      return window['web3'] !== undefined
    }
  }

}
</script>

<style lang="stylus">
  @import './stylus/main'
</style>
