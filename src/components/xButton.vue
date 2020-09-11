<template>
  <button
    @click="btnClick"
    class="bg-transparent hover:bg-green-500 text-green-700 font-semibold hover:text-white py-2 px-2 border border-green-500 hover:border-transparent rounded"
  >
    <beat-loader :loading="isLoading" :color="'#68d391'" :size="8" />
    <slot v-show="!isLoading"></slot>
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
