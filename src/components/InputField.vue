<template>
  <div>
    <input type="text" ref="amountInput" />
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
</template>

<script>
export default {
  data() {
    return {
      data: [],
      currencyKeys: [],
      currencyOne: "",
      currencyTwo: "",
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
    conversionRate() {},
  },
  mounted() {
    this.getCurrencyKeys();
    this.fetchData();
  },
};
</script>
