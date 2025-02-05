<template>
  <table class="bg-table rounded-lg shadow-md">
    <thead>
      <tr class="border-b-2 border-gray-600">
        <th></th>
        <th :class="{ up: this.sortOrder === 1, down: this.sortOrder === -1 }">
          <span class="cursor-pointer" @click="changeSortOrder">
            #
          </span>
        </th>
        <th>Nombre</th>
        <th>Precio</th>
        <th>Cap. de Mercado</th>
        <th>Variación 24hs</th>
        <td class="hidden sm:block">
          <input
            class="bg-gray-100 focus:outline-none border-b border-gray-400 py-2 px-4 block w-full appearance-none leading-normal rounded"
            id="filter"
            placeholder="Buscar..."
            type="text"
            v-model="filter"
          />
        </td>
      </tr>
    </thead>

    <tbody>
      <tr
        v-for="(a, idx) in filteredAssets"
        :key="a.id"
        class="hover:bg-purple-900"
        :class="idx !== filteredAssets.length - 1 && 'border-b border-gray-800'"
      >
        <td>
          <img
            class="w-6 h-6 mx-2 lg:mx-0"
            :src="
              `https://static.coincap.io/assets/icons/${a.symbol.toLowerCase()}@2x.png`
            "
            :alt="a.name"
          />
        </td>
        <td>
          <b># {{ a.rank }}</b>
        </td>
        <td>
          <router-link
            class="font-bold"
            :to="{ name: 'coin-detail', params: { id: a.id } }"
          >
            {{ a.name }}
          </router-link>
          <small class="ml-1 text-gray-500">{{ a.symbol }}</small>
        </td>
        <td class="font-bold">{{ a.priceUsd | dollar }}</td>
        <td class="font-bold">{{ a.marketCapUsd | dollar }}</td>
        <td
          class="font-bold"
          :class="
            a.changePercent24Hr.includes('-')
              ? 'text-red-600'
              : 'text-green-600'
          "
        >
          {{ a.changePercent24Hr | percent }}
        </td>
        <td class="hidden sm:block">
          <x-button @click="goToCoin(a.id)">
            <span>Detalles</span>
          </x-button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import xButton from '@/components/xButton'

export default {
  name: 'xAssetsTable',

  components: { xButton },

  props: {
    assets: {
      type: Array,
      default: () => []
    }
  },

  data() {
    return {
      filter: '',
      sortOrder: 1
    }
  },

  computed: {
    filteredAssets() {
      const altOrder = this.sortOrder === 1 ? -1 : 1

      return this.assets
        .filter(
          a =>
            a.symbol.toLowerCase().includes(this.filter.toLowerCase()) ||
            a.name.toLowerCase().includes(this.filter.toLowerCase())
        )
        .sort((a, b) => {
          if (parseInt(a.rank) > parseInt(b.rank)) {
            return this.sortOrder
          }

          return altOrder
        })
    }
  },

  methods: {
    goToCoin(id) {
      this.$router.push({ name: 'coin-detail', params: { id } })
    },

    changeSortOrder() {
      this.sortOrder = this.sortOrder === 1 ? -1 : 1
    }
  }
}
</script>

<style scoped>
.up::after {
  content: '▲';
}

.down::after {
  content: '▼';
}

td {
  padding: 20px 0px;
  font-size: 0.6rem;
  text-align: center;
}

th {
  padding: 5px;
  font-size: 0.6rem;
}

@media (min-width: 640px) {
  td,
  th {
    padding: 20px;
    font-size: 1rem;
  }

  th {
    padding: 12px;
  }
}

.bg-table {
  background-color: #1F1B3A;
}
</style>
