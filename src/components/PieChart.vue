<script setup>
import { onBeforeMount,onMounted, onBeforeUnmount, ref } from 'vue';

let pieChart = null

// chart data
const data = {
  labels: [
    'Orange',
    'Yellow',
    'Brown'
  ],
  datasets: [{
    data: [30, 40, 30],
    backgroundColor: [
      'orange',
      'yellow',
      'brown'
    ] ,
    hoverOffset: 4
  }]
};

// Pie chart configuration
const pieConfig = {
  type: 'pie',
  data: data,
  options: {
    responsive: true
  }
};


onBeforeMount(() => {
  console.log("Before Mounted")
})

onMounted(() => {
  // Get a reference to the canvas element
  const pieCtx = document.getElementById('myPieChart').getContext('2d');

  // Create the pie chart
  pieChart = new Chart(pieCtx, pieConfig);
})

onBeforeUnmount(() => {
  data.labes = []
  data.datasets = []
})

const colorName = ref('')
const colorParcent = ref('')

function updateChart(){
  data.labels.push(colorName.value)
  data.datasets[0].data.push(colorParcent.value)
  data.datasets[0].backgroundColor.push(colorName.value.toLowerCase())

  pieChart.update()
}
</script>

<template>

  <div class="grid grid-cols-2 gap-6">
    <div class="w-2/3">
      <h1 class="text-2xl text-gray-900 text-center">Pie Chart</h1>
      <canvas id="myPieChart"></canvas>
    </div>
  </div>


  <form>
    <div class="grid gap-6 mb-6 md:grid-cols-3">
      <div>
          <input v-model="colorName" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-yellow-500 focus:border-yellow-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-yellow-500 dark:focus:border-yellow-500" required placeholder="Color Name">
      </div>
      <div>
          <input v-model="colorParcent" type="number" id="color-parcent" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-yellow-500 focus:border-yellow-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-yellow-500 dark:focus:border-yellow-500" required placeholder="Parcent">
      </div>
      <div>
        <button @click.prevent="updateChart()" type="submit" class="text-white bg-yellow-700 hover:bg-yellow-800 focus:ring-4 focus:outline-none focus:ring-yellow-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-yellow-600 dark:hover:bg-yellow-700 dark:focus:ring-yellow-800">Add New Item</button>
      </div>
    
    </div>
  </form>

</template>

<style scoped>

</style>
