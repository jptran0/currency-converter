<template>
  <form @submit.prevent="conversionRate">
    <div class="form-container">
      <input type="text" v-model="amountInput" v-on:keyup="conversionRate" />
      <select
        name="currency"
        id="currency"
        v-model="currencyOne"
        @change="conversionRate"
      >
        <option v-for="key in currencyKeys" :key="key">
          {{ key }}
        </option>
      </select>
      <p>=</p>
      <input type="text" :value="conversion" disabled />
      <select
        name="currency"
        id="currency"
        v-model="currencyTwo"
        @change="conversionRate"
      >
        <option v-for="key in conversionKeys" :key="key">
          {{ key }}
        </option>
      </select>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      data: {},
      currencyKeys: [],
      conversionKeys: [],
      currencyOne: "BTC",
      currencyTwo: "USD",
      amountInput: "1",
      conversion: "",
    };
  },
  methods: {
    fetchRates() {
      return fetch("https://api.bitpanda.com/v1/ticker").then((response) =>
        response.json()
      );
    },
    fetchData() {
      this.fetchRates().then((data) => (this.data = data));
      console.log(this.data);
    },
    getCurrencyKeys() {
      this.fetchRates().then((data) => {
        this.currencyKeys = Object.keys(data);
      });
    },
    getConversionKeys() {
      this.fetchRates().then((data) => {
        this.conversionKeys = Object.keys(data.BTC);
      });
    },
    conversionRate() {
      const rate = this.data[this.currencyOne][this.currencyTwo];
      if (this.currencyTwo === "USD" || this.currencyTwo === "EUR") {
        this.conversion = (parseFloat(this.amountInput) * rate).toFixed(2);
      } else {
        this.conversion = (parseFloat(this.amountInput) * rate).toFixed(12);
      }
    },
  },
  mounted() {
    this.getCurrencyKeys();
    this.fetchData();
    this.getConversionKeys();
  },
};
</script>

<style scoped>
.form-container {
  display: flex;
  justify-content: space-around;
  margin: 25px auto;
}
select {
  width: 80px;
}
</style>
