<script>
export default {
  data() {
    return {
      amount: "",
      category: "0", // Default to "no selection"
      type: "0", // Default to "no selection"
    };
  },
  methods: {
    submitForm() {
      if (this.amount && this.category !== "0" && this.type !== "0") {
        // Emit the transaction data
        this.$emit("add-transaction", {
          amount: this.amount,
          category: this.getCategoryName(this.category),
          type: this.type === "1" ? "Income" : "Expense",
        });

        // Reset form fields
        this.amount = "";
        this.category = "0"; // Reset to "no selection"
        this.type = "0"; // Reset to "no selection"

        // Force Vue to update the dropdown display
        this.$nextTick(() => {
          this.$refs.categoryDropdown.value = "0";
          this.$refs.typeDropdown.value = "0";
        });
      } else {
        alert("Please fill out all fields before submitting.");
      }
    },
    getCategoryName(value) {
      const categories = {
        "1": "Home",
        "2": "Vehicle",
        "3": "Business",
        "4": "Bills & Payments",
        "5": "Grocery/Food",
        "6": "Activities",
      };
      return categories[value];
    },
  },
};
</script>

<template>
  <form @submit.prevent="submitForm" class="transaction-form">
    <input
      type="number"
      v-model="amount"
      placeholder="Enter amount"
      required
      class="input-field"
    />
    <select v-model="category" ref="categoryDropdown" required class="input-field">
      <option value="0" disabled>Select category</option>
      <option value="1">Home</option>
      <option value="2">Vehicle</option>
      <option value="3">Business</option>
      <option value="4">Bills & Payments</option>
      <option value="5">Grocery/Food</option>
      <option value="6">Activities</option>
    </select>
    <select v-model="type" ref="typeDropdown" required class="input-field">
      <option value="0" disabled>Select type</option>
      <option value="1">Income</option>
      <option value="2">Expense</option>
    </select>
    <button type="submit">Add Transaction</button>
  </form>
</template>



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
  background-color: #b300b3;
}
</style>
