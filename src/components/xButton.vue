<template>
  <button
    @click="btnClick"
    class="bg-purple-700 hover:bg-purple-600 text-white-700 font-semibold hover:text-white py-2 px-3 rounded"
  >
    <beat-loader :loading="isLoading" :color="'#8E51C3'" :size="8" />
    <p v-show="!isLoading">
      <slot></slot>
    </p>
  </button>
</template>

<script>
export default {
  name: 'xButton',

  props: {
    isLoading: {
      type: Boolean,
      default: false
    }
  },

  methods: {
    btnClick() {
      this.$emit('click')
    }
  }
}
</script>
