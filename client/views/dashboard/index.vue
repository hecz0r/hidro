<template>
  <div>
    <div class="tile is-ancestor">
      <div class="tile is-parent is-6">
        <article class="tile is-child box">
          <h4 class="title">Preț m<sup>3</sup> apă</h4>
          <div class="content">
            <chart :type="'line'" :data="pretKW"></chart>
          </div>
        </article>
      </div>
      <div class="tile is-parent is-6">
        <article class="tile is-child box">
          <h4 class="title">Consum mediu per cameră</h4>
          <div class="content">
            <chart :type="'pie'" :data="consum"></chart>
          </div>
        </article>
      </div>
      <div class="tile is-parent is-6">
        <article class="tile is-child box">
          <h4 class="title">Facturi plătite</h4>
          <div class="content">
            <chart :type="'line'" :data="platiFacturi"></chart>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>

<script>
import Chart from 'vue-bulma-chartjs'

export default {
  components: {
    Chart
  },

  data () {
    return {
      data: [3.67, 3.84, 4.32, 3.93]
    }
  },

  data2 () {
    return {
      data: [4, 5, 3, 7, 8]
    }
  },

  computed: {
    pretKW () {
      return {
        labels: [
          'Ianuarie',
          'Februarie',
          'Martie',
          'Aprilie'
        ],
        datasets: [{
          data: this.data,
          label: 'București',
          borderColor: [
            'rgba(54, 162, 235, 1)',
            'rgba(255, 206, 86, 1)',
            'rgba(75, 192, 192, 1)',
            'rgba(153, 102, 255, 1)',
            'rgba(255, 159, 64, 1)'
          ]
        }]
      }
    },
    consum () {
      return {
        labels: [
          'Bucătărie',
          'Baie'
        ],
        datasets: [{
          data: [4, 8],
          borderColor: [
            'rgba(54, 162, 235, 1)',
            'rgba(255, 206, 86, 1)',
            'rgba(75, 192, 192, 1)',
            'rgba(153, 102, 255, 1)',
            'rgba(255, 159, 64, 1)'
          ],
          backgroundColor: [
            '#FF6384',
            '#36A2EB',
            '#FFCE56'
          ]
        }]
      }
    },
    platiFacturi () {
      return {
        labels: [
          'Ianuarie',
          'Februarie',
          'Martie',
          'Aprilie'
        ],
        datasets: [{
          data: [86.3, 69.5, 78.1, 91.23],
          label: 'Șoseaua Pantelimon 312',
          borderColor: [
            'rgba(75, 192, 192, 1)',
            'rgba(153, 102, 255, 1)',
            'rgba(255, 159, 64, 1)'
          ]
        }]
      }
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
