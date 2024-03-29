<template>
  <form @submit.prevent="conversionRate">
    <div>
      <input type="text" v-model="amountInput" />
      <select name="currency" id="currency" v-model="currencyOne">
        <option v-for="key in currencyKeys" :key="key">
          {{ key }}
        </option>
      </select>
    </div>
    <p>=</p>
    <div>
      <input type="text" :value="conversion" disabled />
      <select name="currency" id="currency" v-model="currencyTwo">
        <option v-for="key in conversionKeys" :key="key">
          {{ key }}
        </option>
      </select>
      <button>Convert</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      data: {},
      currencyKeys: {},
      conversionKeys: [],
      currencyOne: "BTC",
      currencyTwo: "USD",
      amountInput: "1",
      sampleCurrency: "XAU",
      testData: "",
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
      this.conversion = (parseFloat(this.amountInput) * rate).toFixed(2);
    },
  },
  mounted() {
    this.getCurrencyKeys();
    this.fetchData();
    this.getConversionKeys();
  },
};
</script>
