<template>
  <div id="app">
    <h1>Blockchain workshop</h1>
    <el-input placeholder="Enter your addrees" v-model="input"></el-input>
    <el-button type="primary" @click="getBalance">Check balance</el-button>
    <div>Data:
      <span>ballance: {{balance}} </span>
    </div>
  </div>
</template>

<script>
// import nem from 'nem-sdk';
import axios from 'axios';

export default {
  data() {
    return {
      response: null,
      balance: 0,
      input: '',
    };
  },
  created() {
    const that = this;
    console.log('hello world');
    axios.get('https://adamexperimental.cyberblox.my:7891/account/get?address=TDNDDQNA4PVCUNN2YUBG4BP2FUCGBAETB7ONION2')
      .then((response) => {
        console.log(response);
        that.response = response;
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    getBalance() {
      const that = this;
      const address = this.input;
      axios.get(`https://adamexperimental.cyberblox.my:7891/account/get?address=${address}`)
        .then((response) => {
          console.log(response);
          that.balance = response.data.account.balance;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
