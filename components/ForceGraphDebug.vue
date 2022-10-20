<template>
  <div id="main">
    <div id="corneridentifiers">
      <div id="topleftcorneridentifier">
        <div class="hl"></div>
        <div class="vl"></div>
      </div>
      <div id="toprightcorneridentifier">
        <div class="vl" style="position: absolute; top: 0px; right: 0px"></div>
        <div class="hl"></div>
      </div>
      <div id="bottomrightcorneridentifier">
        <div id="bottomrightcorneridentifier" class="hl"></div>
        <div class="vl"></div>
      </div>
      <div id="bottomleftcorneridentifier">
        <div
          class="hl"
          style="position: absolute; bottom: 0px; left: 0px"
        ></div>
        <div class="vl"></div>
      </div>
    </div>
    <div id="centeridentifier">
      <div
        class="hl"
        style="
          position: absolute;
          top: 50%;
          right: 50%;
          width: 10px;
          border-top: 3px solid blue;
        "
      ></div>
      <div
        class="vl"
        style="
          position: absolute;
          top: 50%;
          right: 50%;
          height: 10px;
          border-left: 3px solid blue;
        "
      ></div>
    </div>
    <div id="thirdsidentifier"></div>
  </div>
</template>

<script>
export default {
  name: 'PortfolioForceGraphDebug',

  data() {
    return {
      // this is the primary canvas object for drawing d3 visualizations
      svg: null,
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

    window.addEventListener("resize", () => {
      this.resizeSVG();
    });
  },

  methods: {
    //Changes the attribute height and width to match the container
    resizeSVG() {
      this.svg = d3
        .select('.datavisualization')
        .attr('width', window.innerWidth)
        .attr('height', window.innerHeight)
    },
  },
}
</script>

<style lang="scss" scoped>
.vl {
  border-left: 6px solid green;
  height: 50px;
}
.hl {
  border-top: 6px solid green;
  width: 50px;
}

#toprightcorneridentifier {
  position: absolute;
  top: 0px;
  right: 0px;
}

#bottomleftcorneridentifier {
  position: absolute;
  bottom: 0px;
  left: 0px;
}
#bottomrightcorneridentifier {
  position: absolute;
  bottom: 0px;
  right: 0px;
}
</style>
