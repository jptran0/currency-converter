<template>
  <form @submit.prevent="getConversion">
    <div>
      <input type="text" v-model="amountInput" />
      <select name="currency" id="currency" v-model="currencyOne">
        <option v-for="key in currencyKeys" :key="key" value="key">
          {{ key }}
        </option>
      </select>
    </div>
    <p>=</p>
    <div>
      <input type="text" disabled />
      <select name="currency" id="currency" v-model="currencyTwo">
        <option v-for="key in currencyKeys" :key="key" value="key">
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
      data: [],
      currencyKeys: [],
      currencyOne: "",
        currencyTwo: "",
      amountInput: ""
    };
  },
  methods: {
    fetchResponse() {
      fetch("https://api.bitpanda.com/v1/ticker")
        .then((response) => response.json())
        .then((data) => (this.data = data));
    },
    getCurrencyKeys() {
      fetch("https://api.bitpanda.com/v1/ticker")
        .then((response) => response.json())
        .then((data) => {
          this.currencyKeys = Object.keys(data);
        });
    },
      conversionRate() { },
      getConversion() {
        const rate =
    }
  },
  mounted() {
    this.getCurrencyKeys();
    this.fetchData();
  },
};
</script>
