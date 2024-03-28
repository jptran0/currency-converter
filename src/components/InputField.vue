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
  <!-- <h3>Test API Here</h3>
  <button @click="testAPI">Test</button> -->
</template>

<script>
export default {
  data() {
    return {
      data: {},
      currencyKeys: [],
      conversionKeys: [],
      specificCurrency: [],
      currencyOne: "",
      currencyTwo: "",
      amountInput: "",
      sampleCurrency: "XAU",
      testData: "",
      conversion: "",
    };
  },
  methods: {
    fetchData() {
      fetch("https://api.bitpanda.com/v1/ticker")
        .then((response) => response.json())
        .then((data) => (this.data = data));
      console.log(this.data);
    },
    getCurrencyKeys() {
      fetch("https://api.bitpanda.com/v1/ticker")
        .then((response) => response.json())
        .then((data) => {
          this.currencyKeys = Object.keys(data);
        });
    },
    getConversionKeys() {
      fetch("https://api.bitpanda.com/v1/ticker")
        .then((response) => response.json())
        .then((data) => {
          this.conversionKeys = Object.keys(data.BTC);
        });
    },
    getSpecificCurrency() {
      fetch("https://api.bitpanda.com/v1/ticker")
        .then((response) => response.json())
        .then((data) => {
          this.specificCurrency = data.BTC;
        });
    },
    conversionRate() {
      const rate = this.data[this.currencyOne][this.currencyTwo];
      this.conversion = parseFloat(this.amountInput) * rate;
    },
    testAPI() {
      console.log(this.currencyKeys);
    },
  },
  mounted() {
    this.getCurrencyKeys();
    this.fetchData();
    this.getSpecificCurrency();
    this.getConversionKeys();
  },
};
</script>
