<template>
  <div class="hello">
          <div id="content">
		  <p> Daily tests per million vs Daily confirmed cases per million </p>
		  <p> Scatter Plot </p>
          <canvas ref="chart"/>
        </div>

  </div>
</template>

<script>
import Chart from "chart.js";
import * as d3 from "d3"; 
//var d3= require ("d3");
export default {
  name: 'HelloWorld',
  data () {
    return {
      data: [{}],
      msg: 'Welcome to Your Vue.js App',
	  points : [{
                x: -10,
                y: 0
            }, {
                x: 0,
                y: 10
            }, {
                x: 10,
                y: 5
            }],
    }
  },
  async mounted() {
    await this.readData();
    await this.scatterPlot();
  },
  methods : {
    async readData() {
	d3.csv("covid-19-daily-tests-vs-daily-new-confirmed-cases.csv").then(function(data) {
  console.log(data[0]);
});
	//var x  = readcsv("filename") {
	//}
	
	//points.push({this.x,this.y});
    //  console.log(this.data)
    },
    async scatterPlot() {
      const chart = this.$refs.chart;
      const ctx = chart.getContext("2d");
      var scatterChart = new Chart(ctx, {
      type: 'scatter',
      data: {
        datasets: [{
            label: 'Scatter Dataset',
            data: this.points,
            borderWidth: 2
        }]
    },
    options: {
        scales: {
            xAxes: [{
                type: 'linear',
                position: 'bottom'
            }]
        }
    }
});

    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
