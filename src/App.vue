<template>
    <div v-if="!submitted || amount === ''" class="container">
      <form @submit.prevent="storeInitialAmount">
        <input type="text" placeholder="Enter in starting amount...." v-model="amount"/>
        <button>Submit Amount</button>
      </form>
    </div>
    <div v-else>
        <BudgetAmounts />
      </div>
</template>

<script>
import BudgetAmounts from './components/BudgetAmounts.vue';

export default {
  name: 'App',
  components: {
    BudgetAmounts
  },
  data() {
    return {
      amount: "",
      submitted: false
    }
  },
  methods: {
    storeInitialAmount() {
      let store = window.localStorage;
      if(this.amount === '') {
        return
      }
      store.setItem('amount', this.amount)
      this.submitted = true
    }
  }
}
</script>

<style scoped>
  .container {
    width: 300px;
    height: 250px;
    margin: 0 auto;
  }

  form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  input {
    font-size: 20px;
    padding: 10px;
    width: 500px;
    outline: none;
  }

  button {
    text-transform: uppercase;
    font-size: 15px;
    font-weight: bold;
    padding: 10px;
    width: 200px;
    cursor: pointer;
  }

  button:hover {
    color: white;
    background-color:limegreen;
  }
</style>
