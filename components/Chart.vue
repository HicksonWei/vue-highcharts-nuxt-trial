<template>
  <section class="charts">
    <h3>Line Basic
      <p>Load data with async</p>
    </h3>
    <vue-highcharts :options="options" :highcharts="Highcharts" ref="lineCharts"></vue-highcharts>
    <button @click="load">load</button>
  </section>
</template>

<script>
import VueHighcharts from 'vue2-highcharts'
import Exporting from "highcharts/modules/exporting.js";
import Drilldown from 'highcharts/modules/drilldown.js'
import Highcharts from "highcharts";
// Drilldown(Highcharts);

Exporting(Highcharts);
export default {
  components: {
    VueHighcharts,
  },
  data() {
    return {
      options: {
        chart: {
          type: "spline"
        },
        title: {
          text: "Monthly Average Temperature"
        },
        subtitle: {
          text: "Source: WorldClimate.com"
        },
        xAxis: {
          categories: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec"
          ]
        },
        yAxis: {
          title: {
            text: "Temperature"
          },
          labels: {
            formatter: function() {
              return this.value + "°";
            }
          }
        },
        tooltip: {
          crosshairs: true,
          shared: true
        },
        credits: {
          enabled: false
        },
        plotOptions: {
          spline: {
            marker: {
              radius: 4,
              lineColor: "#666666",
              lineWidth: 1
            }
          }
        },
        series: []
      },
      Highcharts: Highcharts
    };
  },
  methods: {
    load() {
      let lineCharts = this.$refs.lineCharts;
      //charts.showLoading('loading');

      // you also can use the delegateMethod()
      lineCharts.delegateMethod("showLoading", "Loading...");
      setTimeout(() => {
        lineCharts.addSeries(data.asyncData);
        lineCharts.hideLoading();
      }, 2000);
    }
  }
};
</script>
