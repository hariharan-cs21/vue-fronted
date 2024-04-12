<template>
  <div class="container">
    <header class="header">
      <h1 class="header-title">{{ collegeName }}</h1>
      <div class="header-details">
        <h2>{{ performanceData.studentname }}</h2>
        <p>{{ performanceData.registerNumber }}</p>
      </div>
    </header>

    <div class="main-content">
      <div class="student-info">
        <div class="column">

          <p><strong>Batch:</strong> {{ performanceData.batch }}</p>
          <p><strong>Department:</strong> {{ performanceData.department }}</p>
          <p><strong>Contact: </strong><a href="tel:{{ performanceData.contact }}">{{ performanceData.contact }}</a></p>

        </div>
        <div class="column">
          <p><strong>Email:</strong> {{ performanceData.studentEmail }}</p>
          <p><strong>Undertaking:</strong> {{ performanceData.undertaking }}</p>
        </div>
      </div>

      <div class="chart-container">
        <canvas id="progressChart" width="600" height="300"></canvas>
      </div>
    </div>
  </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
  mounted() {
    const performanceData = JSON.parse(this.$route.query.performanceData);
    if (performanceData) {
      this.performanceData = performanceData;
      this.renderProgressChart();
    } else {
      console.warn('Performance Data is undefined');
    }
  },
  data() {
    return {
      performanceData: {},
      collegeName: "Bannari Amman Institute of Technology"
    };
  },
  methods: {
    renderProgressChart() {
      const ctx = document.getElementById('progressChart').getContext('2d');
      new Chart(ctx, {
        type: 'line',
        data: {
          labels: ['Week 1', 'Week 2', 'Week 3', 'Week 4', 'Week 5'],
          datasets: [{
            label: 'Progress',
            data: [80, 50, 70, 80, 60],
            backgroundColor: 'rgba(54, 162, 235, 0.5)',
            borderColor: 'rgba(54, 162, 235, 1)',
            borderWidth: 1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true,
              ticks: {
                callback: function (value) {
                  return value + '%';
                }
              }
            }
          }
        }
      });
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
}

.header {
  background-color: #f8f9fa;
  padding: 20px 40px;
  border-bottom: 1px solid #e2e6ea;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-title {
  margin: 0;
  font-size: 28px;
  color: #333;
}

.header-details {
  text-align: right;
}

.main-content {
  padding: 40px;
}

.student-info {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 20px;
  margin-bottom: 5px;
}

.column {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}

.column p {
  margin: 5px 0;
}

.column p strong {
  font-weight: bold;
  color: #555555;
}

.chart-container {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}
</style>