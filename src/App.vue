<template>
  <div class="app-container">
    <h1>Finance Tracker</h1>
    <TransactionForm @add-transaction="addTransaction" />
    <ul class="transaction-list">
      <li v-for="(transaction, index) in transactions" :key="index" class="transaction-item">
        <span :class="transaction.type === 'Income' ? 'income' : 'expense'">
          {{ transaction.type === 'Income' ? '+' : '-' }}${{ transaction.amount }}
        </span>
        {{ transaction.category }}
      </li>
    </ul>
    <SummaryChart :transactions="transactions" />
  </div>
</template>

<script>
import TransactionForm from './components/TransactionForm.vue';
import SummaryChart from './components/SummaryChart.vue';

export default {
  components: {
    TransactionForm,
    SummaryChart,
  },
  data() {
    return {
      transactions: [], // Array to hold transactions
    };
  },
  methods: {
    addTransaction(transaction) {
      this.transactions.push(transaction);
    },
  },
};
</script>

<style>
/* Global container for centering content */
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: 'Arial', sans-serif;
  background-color: #f8f9fa;
  padding: 20px;
  box-sizing: border-box;
  text-align: center;
}

h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #333;
}

/* Styling for transaction list */
.transaction-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
  max-width: 500px;
  width: 100%;
}

.transaction-item {
  background: #e0e0e0;
  padding: 15px;
  margin: 10px 0;
  border-radius: 25px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1.2rem;
  transition: background 0.3s ease;
}

.transaction-item:hover {
  background: #d1d1d1;
}

.transaction-item span {
  font-weight: bold;
}

/* Income (Green) */
.income {
  color: #4caf50;
}

/* Expense (Red) */
.expense {
  color: #f44336;
}

/* Styling for the form and inputs */
input,
select {
  border-radius: 25px;
  padding: 10px;
  font-size: 1rem;
  border: 2px solid #ccc;
  margin: 10px 0;
  width: 300px;
  max-width: 100%;
  background-color: #fff;
  transition: all 0.3s ease;
}

input:focus,
select:focus {
  border-color: #007bff;
  outline: none;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 12px 20px;
  font-size: 1rem;
  border-radius: 25px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

/* Styling for the chart container */
.chart-container {
  width: 80%;
  max-width: 600px;
  height: 400px;
  margin-top: 30px;
}

/* For general input field spacing */
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}
</style>

