<template>
  <div>
    <x-assets-table :assets="assets" />
  </div>
</template>

<script>
import xAssetsTable from '@/components/xAssetsTable'
import api from '@/api'

export default {
  name: 'Home',

  components: { xAssetsTable },

  data() {
    return {
      assets: []
    }
  },

  created() {
    api.getAssets().then(assets => {
      console.log(assets)
      this.assets = assets
    })
  }
}
</script>
