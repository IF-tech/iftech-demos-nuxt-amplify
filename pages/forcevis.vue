<template>
  <div>
    <v-btn @click="this.groupByColor">Group By color</v-btn>
    <div id="datavis"></div>
  </div>
</template>

<script>
import * as d3 from 'd3'
export default {
  name: 'PortfolioForcevis',

  data() {
    return {
      data: [1, 2, 3, 4, 5],
      svg: null,
      nodes: [
        { color: 'red', size: 10 },
        { color: 'red', size: 15 },
        { color: 'red', size: 20 },
        { color: 'blue', size: 10 },
        { color: 'blue', size: 15 },
        { color: 'blue', size: 20 },
        { color: 'yellow', size: 10 },
        { color: 'yellow', size: 15 },
        { color: 'yellow', size: 20 },
      ],
      width: null,
      height: null,
      simulation: null,
      forceField: null,
    }
  },

  mounted() {

    this.width = window.innerWidth
    this.height = window.innerHeight
    //Initialize svg to datavis element, assigning the width and height to be the height of the inner window
    this.svg = d3
      .select('#datavis')
      .append('svg')
      .classed('datavisualization', true)
      .attr('width', this.width)
      .attr('height', this.height)

    // listen for resize of the window
    window.addEventListener('resize', () => {
      this.resizeSVG()
      // this.drawForceNodes()
      this.updateForces()
    })

    this.initializeSimulation()
    this.drawForceNodes()
    this.simulation.alpha(1).restart()
  },

  methods: {
    groupByColor(){
      let height = window.innerHeight
      let width = window.innerWidth
      const colorNodePositions = {
          red: { x: 500, y: height / 3 },
          blue: { x: 800, y: (height / 3)*2},
          yellow: { x: 1000, y: (height / 3)*2 },
        };

        function nodeXPos(d) {
          return colorNodePositions[d.color].x;
        }
        function nodeYPos(d) {
          return colorNodePositions[d.color].y;
        }


        this.simulation.force(
          "x",
          d3.forceX().strength(0.3).x(nodeXPos)
        );

        this.simulation.force(
          "y",
          d3.forceY().strength(0.03).y(nodeYPos)
        );

    },
    resizeSVG() {
      this.svg = d3
        .select('.datavisualization')
        .attr('width', window.innerWidth)
        .attr('height', window.innerHeight)
    },
    initializeSimulation() {
      let nodes = this.nodes

      const fillColor = d3
        .scaleOrdinal()
        .domain(['red', 'blue', 'yellow'])
        .range(['red', 'blue', 'yellow'])

      this.simulation = d3
        .forceSimulation(nodes)
        .force('charge', d3.forceManyBody().strength(-20))
        // .force('center', d3.forceCenter(window.innerWidth / 2, window.innerHeight / 2))
        .force(
          'x',
          d3
            .forceX()
            .strength(0.1)
            .x(window.innerWidth / 2)
        )
        .force(
          'y',
          d3
            .forceY()
            .strength(0.1)
            .y(window.innerHeight / 2)
        )
        .on('tick', ticked)

      let bubbles = d3
        .select('svg')
        .append('g')
        .classed('bubbles', true)
        .selectAll('circle')
        .data(nodes)
        .join('circle')
        .attr('r', function (d) {
          return d.size
        })
        .attr('fill', function (d) {
          return fillColor(d.color)
        })
        .attr('cx', function (d) {
          return d.x
        })
        .attr('cy', function (d) {
          return d.y
        })

      function ticked() {
        bubbles
          .attr('cx', function (d) {
            return d.x
          })
          .attr('cy', function (d) {
            return d.y
          })
      }
    },
    drawForceNodes() {
      let height = window.innerHeight
      let width = window.innerWidth
      let forceNodes = [{ name: 'center' }]
      d3.select('.forceNodes').remove()
      let forceCircles = d3
        .select('.datavisualization')
        .append('g')
        .classed('forceNodes', true)
        .data(forceNodes)
      forceCircles
        .append('circle')
        .classed('forceNode', true)
        .attr('r', 5)
        .attr('fill', 'green')
        .attr('cx', width / 2)
        .attr('cy', height / 2)
    },
    updateForces() {
      let height = window.innerHeight
      let width = window.innerWidth
      this.simulation.force(
        'y',
        d3
          .forceY()
          .strength(0.04)
          .y(height / 2)
      )
      this.simulation.force(
        'x',
        d3
          .forceX()
          .strength(0.04)
          .x(width / 2)
      )
      //We can reset the alpha value and restart the simulation
      this.simulation.alpha(1).restart()
    },
  },
}
</script>

<style lang="scss" scoped>
circle {
  fill: cadetblue;
}
</style>
