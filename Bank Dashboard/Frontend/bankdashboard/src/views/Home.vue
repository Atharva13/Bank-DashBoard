<template>
  <v-container class="mt-3">
    <h4 class="headline font-weight-bold ml-5">
      Savings Account
    </h4>
    <List :accountData="savings"/>

    <h4 class="headline font-weight-bold ml-5">
      Fixed Deposits
    </h4>
    <List :accountData="fixeddeposits"/>
  </v-container>
</template>

<script>
import List from '../components/List.vue';

async function fetchData() {
  const url = "http://localhost:3000/";

  const response = await fetch(url, {
    method: "GET",
    cache: "no-cache",
    headers: {
      "Content-Type": "application/json"
    }
  });
  const commits = await response.json();
  return commits;
}
export default {
  name: "Lists",
  components: {
    List
  },
  data: () => ({
    savings: [],
    fixeddeposits: []
  }),
  methods: {
    async fetchAccounts() {
      const accounts = await fetchData();
      this.savings = accounts["savings"];
      this.fixeddeposits = accounts["fixeddeposits"];
    }
  },
  mounted() {
    this.fetchAccounts();
  }
};
</script>