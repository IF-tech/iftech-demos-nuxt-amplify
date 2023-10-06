<template>
  <div id="datavis"></div>
</template>

<script>
import * as d3 from 'd3'
export default {
  name: 'PortfolioBubblevis',
  data() {
    return {
      // this is the primary canvas object for drawing d3 visualizations
      svg: null,
      data: null,
      nodes: null,
      bubbles: null,
      charge: -20,
      simulation: null,
    }
  },
  mounted() {
    //Initialize svg to datavis element, assigning the width and height to be the height of the inner window
    this.svg = d3
      .select('#datavis')
      .append('svg')
      .classed('datavisualization', true)
      .attr('width', window.innerWidth)
      .attr('height', window.innerHeight)

    //listen for resize of the window
    window.addEventListener('resize', () => {
      this.resizeSVG()
    })

    //load in json format
    const FILEPATH =
      'https://iftechpublicassets.s3.us-west-2.amazonaws.com/resumedatawithimages.json'
    d3.json(FILEPATH).then((json) => {
      this.data = json
      //IMPORTANT
      //process the imported data to the shape of a node for the graph
      this.nodes = this.processDataIntoNodes(this.data)

      let bubbles = this.generateBubbles(this.nodes)

      this.initializeSimulation(bubbles)
      this.groupBubblesOnCenter()
    })
  },

  methods: {
    //Changes the attribute height and width to match the container
    resizeSVG() {
      this.svg = d3
        .select('.datavisualization')
        .attr('width', window.innerWidth)
        .attr('height', window.innerHeight)
    },
    //takes in raw json data and maps the values to well-formatted and regularized nodes
    processDataIntoNodes(data) {
      // Use the max size_score in the data as the max in the scale's domain
      // note we have to ensure the size_score is a number.
      const maxAmount = 100

      //determine maximum circle radius dependent on window size
      let rangeMax
      if (window.innerWidth < 500 || window.innerHeight < 500) {
        rangeMax = 36
      } else {
        rangeMax = 50
      }

      //IMPORTANT FUNCTION
      //Scales the radius of the bubbles. There are many options. https://www.d3indepth.com/scales/
      const radiusScale = d3
        .scalePow()
        .exponent(0.5)
        .range([2, rangeMax])
        .domain([0, maxAmount])

      //Use map() https://www.w3schools.com/jsref/jsref_map.asp to convert raw data into node data.
      //Could generalize by getting list of data atrtibutes and then matching the map 1:1 maybe?
      let myNodes = data.map(function (d) {
        return {
          id: d.id,
          radius: radiusScale(+d.size_score),
          value: +d.size_score,
          name: d.tool_name,
          group: d.group,
          year: d.start_year,
          imagelink: d.imagelink,
          x: Math.random() * window.innerWidth,
          y: Math.random() * window.innerHeight,
        }
      })

      myNodes.sort(function (a, b) {
        return b.value - a.value
      })
      return myNodes
    },
    generateBubbles() {
      const fillColor = d3
        .scaleOrdinal()
        .domain(['development', 'data', 'design'])
        .range(['#ffffff', '#d4d4d4', '#a8a8a8'])

      let bubbles = this.svg
        .selectAll('g')
        .classed('bubbles', true)
        .data(this.nodes, function (d) {
          return d.id
        })

      let bubblesEnter = bubbles
        .enter()
        .append('g')
        .attr('class', 'bubblenode')
        .append('circle')
        .classed('bubble', true)
        .attr('r', 0)
        .attr('opacity', 0.9)
        .attr('fill', function (d) {
          return fillColor(d.group)
        })

      bubbles = bubbles.merge(bubblesEnter)

      // Transition to make bubbles appear
      bubbles
        .transition()
        .duration(2000)
        .attr('r', function (d) {
          return d.radius
        })

      return bubbles
    },
    groupBubblesOnCenter() {
      let width = window.innerWidth
      let height = window.innerHeight
      console.log('bubbles grouping')
      console.log(this.simulation)
      // Reset the 'x' force to draw the bubbles to the center.
      this.simulation.force(
        'x',
        d3
          .forceX()
          .strength(0.03)
          .x(width / 1.5)
      )
      this.simulation.force(
        'y',
        d3
          .forceY()
          .strength(0.03)
          .y(height / 2.5)
      )
      //We can reset the alpha value and restart the simulation
      this.simulation.alpha(1).restart()
    },
    initializeSimulation(bubbles) {
      let width = window.innerWidth
      let height = window.innerHeight
      function charge(d) {
        return -Math.pow(d.radius, 2.05) * 0.03
      }
      function ticked() {
        bubbles
          .attr('x', function (d) {
            return d.x
          })
          .attr('y', function (d) {
            return d.y
          })
      }
      //create simulation. velocity decay determines rapidness of animation
      this.simulation = d3
        .forceSimulation()
        .velocityDecay(0.2)
        .force(
          'x',
          d3
            .forceX()
            .strength(0.03)
            .x(width / 1.5)
        )
        .force(
          'y',
          d3
            .forceY()
            .strength(0.03)
            .y(height / 2)
        )
        .force('charge', d3.forceManyBody().strength(charge))
        //this force ensures bubbles do not overlap. comment out for overlapping effect which allows bubbles to move more freely past each other
        // .force("collide", d3.forceCollide(function(d) {
        //   return d.radius;
        // }))
        .on('tick', ticked)

      // Set the simulation's nodes to our newly created nodes array.
      this.simulation.nodes(this.nodes)
    },
  },
}
</script>

