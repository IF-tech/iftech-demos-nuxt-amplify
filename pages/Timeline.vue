<template>
  <v-container>
  <div class="spacer"> </div>
    <div class="spacer">
    <div class="animated-element">
      <h2>animate me</h2>
      <p>This is a card title</p>
      </div>
  </div>
  <div class="spacer"></div>
</v-container>
</template>


<script>
const { gsap } = require("gsap/dist/gsap");
const { ScrollTrigger } = require("gsap/dist/ScrollTrigger");
import Lenis from '@studio-freight/lenis'


gsap.registerPlugin(ScrollTrigger);


export default {
  name: 'LiveTimeline',

  data() {
    return {

    };
  },

  mounted() {
    let tl = gsap.timeline({
      scrollTrigger: {
        trigger: '.animated-element',
        start: 'top center',
        end: 'bottom center',
        scrub: true,
        markers: false,

      }
    })
    tl.to('.animated-element', {
      x:800
    })



    const lenis = new Lenis()

lenis.on('scroll', (e) => {
  // console.log(e)
})

function raf(time) {
  lenis.raf(time)
  requestAnimationFrame(raf)
}

requestAnimationFrame(raf)

  },

  methods: {

  },
};
</script>

<style lang="scss" scoped>
body{
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  font-size: 24px;
  color:white
}

.spacer{
  height: 100vh
}

.animated-element {
  width: 300px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  background-color: #9400df;
  border-radius: 8px;
  box-shadow: 0px 4px 8px rgba(0,0,0,0.2);
  position: relative;
  left: -400px;
}
h2 {
  margin: 0;
  padding: 0;
}

p {
  font-size: .85em;
  line-height: 1.4em;
  margin-bottom: 0;
}

</style>
