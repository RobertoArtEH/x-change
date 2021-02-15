<template>
  <main id="app">
    <x-header :links="links" />

    <router-view class="container px-5 py-10 flex justify-center" />
  </main>
</template>

<script>
import xHeader from '@/components/xHeader'

export default {
  name: 'App',
  components: { xHeader },

  data() {
    return {
      links: [
        {
          title: 'BTC',
          to: { name: 'coin-detail', params: { id: 'bitcoin' } }
        },
        {
          title: 'ETH',
          to: { name: 'coin-detail', params: { id: 'ethereum' } }
        },
        {
          title: 'XRP',
          to: { name: 'coin-detail', params: { id: 'ripple' } }
        }
      ]
    }
  }
}
</script>

<style>
body {
  background-color: #1A1537;
  color: #fff;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
