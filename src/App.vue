<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransactions from './components/AddTransactions.vue';

import { ref, computed } from 'vue';

const transactions = ref([
  {
    id: 1, text: "Sketch Pen", amount: -19.00
  },
  { id: 2, text: "Salary", amount: +21.00 },
  { id: 3, text: "Books", amount: +34.00 },
  { id: 4, text: "Notepad", amount: -5.12 }
]);

// total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
  // acc will start at 0
})

// income
const income = computed(() => {
  return transactions.value.filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
  // acc will start at 0
})


// expenses
const expenses = computed(() => {
  return transactions.value.filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
  // acc will start at 0
})

</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    // + sign to convert them into numbers or else type check for prop will throw warning
    <TransactionList :transactions="transactions" />
    <AddTransactions />
  </div>
</template>
