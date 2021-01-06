<template>
  <img
    alt="logo"
    src="https://arweave.net/lIXEwj6WL4V1ZR_hJjlhsziZp4IVnJQS52rpD0xOvJ4"
  />
  <form v-on:submit.prevent="search">
    <input
      name="transaction_id"
      v-model.trim="searchBar"
      placeholder="Type a transaction id"
    />
  </form>
  <transaction :data="transaction" :tags="tags" />
</template>

<script>
import Transaction from "./components/Transaction.vue";
import Arweave from "arweave";

export default {
  name: "App",
  components: {
    Transaction
  },
  data() {
    return {
      searchBar: "hKMMPNh_emBf8v_at1tFzNYACisyMQNcKzeeE1QE9p8",
      transaction: {},
      tags: {}
    };
  },
  methods: {
    async getTransaction(_id) {
      const arweave = Arweave.init();
      arweave.transactions
        .get(_id)
        .then(res => {
          this.transaction = {
            id: res.id,
            last_tx: res.last_tx,
            quantity: res.quantity,
            data_size: res.data_size
          };
          this.tags = res.tags;
        })
        .catch(() => {
          this.transaction = {};
        });
    },
    search(e) {
      console.log(e.target.transaction_id.value);
      this.getTransaction(e.target.transaction_id.value);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  width: 200px;
  margin-top: -120px;
  margin-bottom: 30px;
}

table {
  width: 500px;
  border-collapse: collapse;
  text-align: left;
  font-family: monospace;
}
td,
th {
  border: 1px solid black;
}
</style>
