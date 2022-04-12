<template>
  <main>
    <div class="container-fluid">
      <div class="p-5">
        <h1 class="title-table fs-1">Precios Bitcoins</h1>
        <table class="table table-hover">
          <thead>
            <tr class="bg-secondary fw-bold fs-5">
              <td>#</td>
              <td>Nombre</td>

              <td>Valor actual</td>
              <td>24hrs</td>
              <td class="text-end">24h Volumen</td>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(data, index) in coins"
              :key="data.name"
              class="color-celda"
              v-on:click="searchData(data)"
            >
              <td>{{ index + 1 }}</td>
              <td>
                <img
                  :src="data.image"
                  :alt="data.name"
                  style="width: 2rem"
                  class="me-2"
                />
                {{ data.name }} <b class="text-uppercase">{{ data.symbol }}</b>
              </td>

              <td>{{ data.current_price.toLocaleString() }}</td>
              <td>{{ data.price_change_24h.toLocaleString() }}</td>
              <td class="text-end">{{ data.total_volume.toLocaleString() }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      coins: [],
    };
  },
  async mounted() {
    const type = "USD";
    const res = await fetch(`
   https://api.coingecko.com/api/v3/coins/markets?vs_currency=${type}&order=market_cap_desc&per_page=100&page=1&sparkline=false`);
    const data = await res.json();
    this.coins = data;
    console.log(data);
  },
  methods: {
    searchData: function (data) {
      console.log(data);
    },
  },
};
</script>
<style></style>
