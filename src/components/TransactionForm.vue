<template>
  <form @submit.prevent="submitForm" class="transaction-form">
    <input
      type="number"
      v-model="amount"
      placeholder="Enter amount"
      required
      class="input-field"
    />
    <select v-model="category" required class="input-field">
      <option value="" disabled>Select category</option>
      <option value="Home">Home</option>
      <option value="Vehicle">Vehicle</option>
      <option value="Business">Business</option>
      <option value="Bills & Payments">Bills & Payments</option>
      <option value="Grocery/Food">Grocery/Food</option>
      <option value="Activities">Activities</option>
    </select>
    <select v-model="type" required class="input-field">
      <option value="" disabled>Select type</option>
      <option value="Income">Income</option>
      <option value="Expense">Expense</option>
    </select>
    <button type="submit">Add Transaction</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      amount: "",
      category: "",
      type: "",
    };
  },
  methods: {
    submitForm() {
      // Only submit if all fields have values
      if (this.amount && this.category && this.type) {
        // Emit the new transaction object
        this.$emit("add-transaction", {
          amount: this.amount,
          category: this.category,
          type: this.type,
        });

        // Reset all fields after submission
        this.amount = "";
        this.category = ""; // Reset category dropdown
        this.type = ""; // Reset type dropdown
      } else {
        alert("Please fill out all fields before submitting.");
      }
    },
  },
};
</script>

<style scoped>
.transaction-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 400px;
  width: 100%;
  margin-top: 20px;
}

.input-field {
  border-radius: 25px;
  padding: 10px;
  margin: 10px 0;
  width: 100%;
  max-width: 300px;
  font-size: 1rem;
  border: 2px solid #ccc;
  background-color: #fff;
  transition: border-color 0.3s ease;
}

.input-field:focus {
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
</style>
