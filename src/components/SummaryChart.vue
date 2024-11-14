<template>
  <div>
    <pie-chart :chart-data="pieChartData" :options="chartOptions" />
  </div>
</template>

<script>
import { Pie } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale);

export default {
  components: {
    PieChart: Pie,
  },
  props: {
    transactions: Array,  // Pass the transactions array as a prop
  },
  computed: {
    // Prepare the data for the pie chart
    pieChartData() {
      const categories = ['Home', 'Vehicle', 'Business', 'Bills & Payments', 'Grocery/Food', 'Activities'];
      const spendingData = categories.map(category => {
        return this.transactions
          .filter(transaction => transaction.category === category && transaction.type === 'Expense')
          .reduce((sum, transaction) => sum + parseFloat(transaction.amount), 0);
      });

      return {
        labels: categories,
        datasets: [
          {
            label: 'Spending Distribution',
            data: spendingData,
            backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#9966FF', '#FF9F40'],
          },
        ],
      };
    },
    chartOptions() {
      return {
        responsive: true,
        plugins: {
          legend: {
            position: 'top',
          },
          tooltip: {
            callbacks: {
              label: function (context) {
                return `${context.label}: $${context.raw.toFixed(2)}`;
              },
            },
          },
        },
      };
    },
  },
};
</script>



  