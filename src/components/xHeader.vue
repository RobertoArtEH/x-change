<template>
  <header class="shadow-lg sticky">
    <nav>
      <nav class="flex items-center justify-around flex-wrap bg-header p-6">
        <div class="flex items-center flex-shrink-0 text-white flex-grow">
          <router-link
            :to="{ name: 'home' }"
            class="font-semibold text-xl tracking-tight"
          >
            <img class="h-8" src="../assets/images/xchange.svg" />
          </router-link>
        </div>
        <div class="sm:block lg:flex lg:items-center lg:wauto">
          <div class="text-sm lg:flex-grow">
            <router-link
              v-for="l in links"
              :key="l.title"
              :to="l.to"
              class="block mt-4 inline-block lg:mt-0 text-white mr-4 font-bold"
            >
              {{ l.title }}
            </router-link>
          </div>
        </div>
      </nav>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'xHeader',

  props: {
    links: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style>
img {
  pointer-events: none;
}

.bg-header {
  background-color: #181533;
}
</style>
