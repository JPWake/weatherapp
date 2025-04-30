<template>
<div class="chart-container" style="position: relative; height:40vh; width:80vw">
  <canvas id="myChart"></canvas>
</div>
</template>







<script>
import Chart from 'chart.js/auto';

export default {

  name: 'GraphChart',
  props: {
    msg: String
  },
  
// this is the actual line graph. hourly data needs to be placed into here.
  
  mounted() {
  const ctx = document.getElementById('myChart');
  const myChart = new Chart(ctx, {
    // the build of the actual graph, settings, styles, info, etc
    type: 'line',
    data: {
        labels: [1,2,3,4,5,],
        datasets: [{
            label: 'Hourly Tempature Rates',
            data: [3, 5, 10, 5, 8,],
            fill: true,
            tension: 0.5,
            backgroundColor: 'rgba(255, 99, 132, 0.2)',
            borderColor: 'rgba(255, 99, 132, 1)',
            borderWidth: 3
        }]
    },
    options: {
      responsive: true,
    }
});


// calling it here so it appears.
myChart;

}};

</script>