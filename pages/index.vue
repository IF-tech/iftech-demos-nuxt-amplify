<template>
  <div>
    <v-container fluid style="position: absolute; z-index: 5; height: 20vh">
      <v-row>
        <v-col>
          <v-img
            src="https://iftechpublicassets.s3.us-west-2.amazonaws.com/static-public-images/iftechLogo.svg"
            alt=""
          ></v-img>
        </v-col>
      </v-row>

      <v-row justify-center align-items="center"
        ><v-spacer></v-spacer
        ><v-col align-self="end">
          <v-btn size="large" color="#ffffff" outlined to="/services/all"
            >Browse Services</v-btn
          ></v-col
        >
        <v-col>
          <v-btn color="#ffffff" outlined to="/about"
            >About ifTech</v-btn
          ></v-col
        ><v-spacer></v-spacer
      ></v-row>
      <div class="spacer red"></div>
      <div class="development">
        <v-row
          ><v-col><h1>DEVELOPMENT</h1></v-col
          ><v-col
            ><v-row><h3>Websites, Apps, Games</h3></v-row
            ><v-row>
              <p>Rapid, Structured, affordable software development</p></v-row
            >
            <v-btn to="/services/dev">Learn More</v-btn>
          </v-col>
        </v-row>
      </div>
      <div class="spacer blue"></div>
      <div class="development">
        <v-row
          ><v-col><h1>DATA</h1></v-col
          ><v-col
            ><v-row><h3>DB Design, Cleaning, Analytics</h3></v-row
            ><v-row> <p>Unlock the true potential of your datasets</p></v-row>
            <v-btn to="/services/data">Learn More</v-btn>
          </v-col>
        </v-row>
      </div>
      <div class="spacer"></div>
      <div class="spacer yellow"></div>
      <div class="development">
        <v-row
          ><v-col><h1>DESIGN</h1></v-col
          ><v-col
            ><v-row><h3>Branding, Graphics, Illustration, Sound</h3></v-row
            ><v-row
              ><p>
                Stand out from the crowd with custom barnding and assets
              </p></v-row
            >
            <v-btn to="/services/data">Learn More</v-btn>
          </v-col>
        </v-row>
      </div>
      <div class="spacer"></div>
    </v-container>

    <canvas class="webgl"></canvas>
  </div>
</template>

<script>
const { gsap } = require('gsap/dist/gsap')
const { ScrollTrigger } = require('gsap/dist/ScrollTrigger')
import Lenis from '@studio-freight/lenis'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
gsap.registerPlugin(ScrollTrigger)

import Services from '../components/Services.vue'

export default {
  layout: 'clear',
  name: 'LiveHeroPage',

  data() {
    return { backgroundColor: '#6de8e6' }
  },

  mounted() {
    this.init()

    const devitemtl = gsap.timeline({
      scrollTrigger: {
        trigger: '.red',
        start: 'top center',
        end: 'bottom center',
        scrub: true,
        // markers: true,
      },
    })
    devitemtl.to('.development', {
      x: '1%',
    })

    const redtl = gsap.timeline({
      scrollTrigger: {
        trigger: '.red',
        start: 'top center',
        end: 'bottom center',
        scrub: true,
        // markers: true,
      },
    })

    redtl.to(this, {
      backgroundColor: '#ff5733',
      duration: 2, // Adjust the duration as needed
      ease: 'power2.inOut', // Adjust the easing function as needed
      // Delay between color changes
    })

    const bluetl = gsap.timeline({
      scrollTrigger: {
        trigger: '.blue',
        start: 'top center',
        end: 'bottom center',
        scrub: true,
        // markers: true,
      },
    })

    bluetl.to(this, {
      backgroundColor: '#32a852',
      duration: 2, // Adjust the duration as needed
      ease: 'power2.inOut', // Adjust the easing function as needed
      // Delay between color changes
    })

    const yellowtl = gsap.timeline({
      scrollTrigger: {
        trigger: '.yellow',
        start: 'top center',
        end: 'bottom center',
        scrub: true,
        // markers: true,
      },
    })

    yellowtl.to(this, {
      backgroundColor: '#f0e922',
      duration: 2, // Adjust the duration as needed
      ease: 'power2.inOut', // Adjust the easing function as needed
      // Delay between color changes
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
    init: function () {
      /**
       * Sizes
       */
      const sizes = {
        width: window.innerWidth,
        height: window.innerHeight,
      }

      window.addEventListener('resize', () => {
        // Update sizes
        sizes.width = window.innerWidth
        sizes.height = window.innerHeight

        // Update camera
        camera.aspect = sizes.width / sizes.height
        camera.updateProjectionMatrix()

        // Update renderer
        renderer.setSize(sizes.width, sizes.height)
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
      })

      let cube, pyramid, sphere

      // Canvas
      const canvas = document.querySelector('canvas.webgl')

      // Scene
      const scene = new THREE.Scene()
      scene.background = new THREE.Color(this.backgroundColor)
      scene.fog = new THREE.Fog(this.backgroundColor, 60, 100)

      // Lights

      let hemiLight = new THREE.HemisphereLight(0xffffff, 0xffffff, 0.4)
      hemiLight.position.set(100, 100, 100)
      // Add hemisphere light to scene

      let d = 10.25
      let pointd = 18.25
      // Add lights
      // Add hemisphere light to scene

      let ambientLight = new THREE.AmbientLight(0xffffff, 0.25)

      let dirLight = new THREE.DirectionalLight(0xffffff, 0.6)
      dirLight.color.setHSL(0, 0.5, 0.95)
      dirLight.position.set(-50, 50, 30)
      dirLight.castShadow = false
      dirLight.shadow.radius = 2
      dirLight.shadow.mapSize = new THREE.Vector2(500, 500)
      dirLight.shadow.camera.near = 0.1
      dirLight.shadow.camera.far = 1500
      dirLight.shadow.camera.left = d * -1
      dirLight.shadow.camera.right = d
      dirLight.shadow.camera.top = d
      dirLight.shadow.camera.bottom = d * -1

      scene.add(hemiLight)
      scene.add(dirLight)
      // scene.add(ambientLight);

      /**
       * Camera
       */
      // Base camera
      const camera = new THREE.PerspectiveCamera(
        50,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      )
      camera.position.z = 55
      camera.position.x = 0
      camera.position.y = 15
      camera.rotation.x = -0.3
      scene.add(camera)

      // Add Floor Geometry
      let floorGeometry = new THREE.PlaneGeometry(500, 500, 1, 1)
      let floorMaterial = new THREE.MeshPhongMaterial({
        color: this.backgroundColor,
        shininess: 10,
      })

      let floor = new THREE.Mesh(floorGeometry, floorMaterial)
      floor.rotation.x = -0.5 * Math.PI
      floor.receiveShadow = true
      floor.position.y = -11
      scene.add(floor)

      const renderer = new THREE.WebGLRenderer({
        canvas: canvas,
      })
      renderer.setSize(sizes.width, sizes.height)
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
      renderer.setClearColor(new THREE.Color('#32a852'), 1)

      const loader = new GLTFLoader()

      // Create an array to hold the cubes
      const cubes = []

      // Cube parameters
      const cubeCount = 50

      // Create cubes and add them to the scene
      for (let i = 0; i < cubeCount; i++) {
        const cubeSize = Math.random() * 4 + 1
        // Geometry and material for the cube
        const geometry = new THREE.BoxGeometry(cubeSize, cubeSize, cubeSize)
        const material = new THREE.MeshStandardMaterial({ color: '#90fc03' }) // Set your desired color

        // Create the cube mesh
        const cube = new THREE.Mesh(geometry, material)

        // Randomly position the cube within a range
        cube.position.x = (Math.random() - 0.5) * 100 // Adjust the range as needed
        cube.position.y = (Math.random() - 0.5) * 100
        cube.position.z = (Math.random() - 0.5) * 100

        // Randomly rotate the cube
        cube.rotation.x = Math.random() * Math.PI * 2
        cube.rotation.y = Math.random() * Math.PI * 2
        cube.rotation.z = Math.random() * Math.PI * 2

        // Add the cube to the scene
        scene.add(cube)

        // Store the cube in the array
        cubes.push(cube)

        gsap.to(scene, {
          duration: 2,
          background: '#32a0a8',
        })

        // Animate the cube to its final position within the scene using GSAP
        gsap.to(cube.position, {
          duration: 2, // Adjust the duration as needed
          x: Math.random() * 60 - 30,
          y: Math.random() * 60 - 20,
          z: Math.random() * 60 - 20,
          ease: 'power2.inOut', // Adjust the easing function as needed
          delay: i * 0.05, // Delay each cube's animation to stagger them
        })
      }

      // Animation function to spin the cubes
      const animateCubes = () => {
        cubes.forEach((cube) => {
          cube.rotation.x += 0.01 // Adjust the rotation speed as needed
          cube.rotation.y += 0.01
          cube.rotation.z += 0.01
        })

        // Render the scene
        renderer.render(scene, camera)

        // Call the animation function on the next frame
        requestAnimationFrame(animateCubes)
      }

      // Start the cube animation
      animateCubes()

      const tick = () => {
        scene.background = new THREE.Color(this.backgroundColor)
        scene.fog = new THREE.Fog(this.backgroundColor, 60, 100)
        cubes.forEach((cube) => {
          cube.material.color = new THREE.Color(this.backgroundColor)
        })
        floor.material.color = new THREE.Color(this.backgroundColor)

        // Render
        renderer.render(scene, camera)
        // Call tick again on the next frame
        const time = Date.now() * 0.001

        requestAnimationFrame(tick)
      }

      tick()

      const animateBackgroundColor = () => {
        // Define the color values you want to animate between
        const colors = ['#a2a4eb', '#32a852', '#ff5733'] // Add more colors as needed

        // Create a GSAP timeline to animate the background color
        const timeline = gsap.timeline()

        // Loop through the colors and add background color animations
        colors.forEach((color, index) => {
          timeline.to(this, {
            backgroundColor: color,
            duration: 2, // Adjust the duration as needed
            ease: 'power2.inOut', // Adjust the easing function as needed
            delay: index * 0.02, // Delay between color changes
          })
        })
      }

      // animateBackgroundColor()
    },
  },
  components: { GLTFLoader, Services },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Libre+Barcode+39+Extended+Text&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Gabarito:wght@500&display=swap');
</style>

<style lang="scss" scoped>
.development {
  font-family: 'Gabarito';
  color: whitesmoke;
  font-size: 3em;
}
.data {
  font-family: 'Libre Barcode 39 Extended Text', cursive;
  color: whitesmoke;
  font-size: 3em;
}

.design {
  font-family: 'Libre Barcode 39 Extended Text', cursive;
  color: whitesmoke;
  font-size: 3em;
}
.small-spacer {
  height: 10vh;
}
.spacer {
  height: 100vh;
}

canvas {
  position: fixed;
  height: 100vh;
  width: 100vw;
}
</style>

