<template>
  <!DOCTYPE html>
  <html lang="en">
    <body>
      <div class="container">
        <!-- <div class="content">
          <h1>iftech</h1>
          <h3>TECHNOLOGY & DESIGN</h3>
          <hr />
        </div>
        <div style="padding-left: 24%; padding-top: 10px" class="buttons">
          <h1>Simple hover effects with <code>box-shadow</code></h1>
            <button class="fill">Fill In</button>
            <button class="pulse">Pulse</button>
            <button class="close">Close</button>
            <button class="raise">Raise</button>
            <button class="up">Fill Up</button>
            <button class="slide">Slide</button>
          <button class="offset">Enter</button>
        </div> -->
<!--
        <div class="content">
          <h3 style="font-size: .7em; margin-left:50%">A (p,q)-torus knot is obtained by looping a string through the hole of a torus p times with q revolutions before joining its ends, where p and q are relatively prime. A (p,q)-torus knot is equivalent to a (q,p)-torus knot. All torus knots are prime (Hoste et al. 1998, Burde and Zieschang 2002). Torus knots are all chiral, invertible, and have symmetry group D_1 (Schreier 1924, Hoste et al. 1998).</h3>
        </div> -->
      </div>

      <canvas class="webgl"></canvas>
    </body>
  </html>
</template>

<script>
import * as THREE from "three";
// import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
import { ObjectLoader } from "three";

export default {
  name: "Home",
  components: {},
  data() {
    return {
    };
  },
  methods: {
    init: function () {
      //obj loader
      const objLoader = new ObjectLoader();

      // Texture Loader

      const star = new THREE.TextureLoader().load("https://iftechpublicassets.s3.us-west-2.amazonaws.com/static-public-images/star.png");

      // Debug
      // const gui = new dat.GUI();
      // dat.GUI.toggleHide();

      // Canvas
      const canvas = document.querySelector("canvas.webgl");

      // Scene
      const scene = new THREE.Scene();

      // Objects
      // const geometry = new THREE.TorusGeometry(0.7, 0.2, 16, 100);
      const geometry = new THREE.TorusKnotGeometry(0.5, 0.18, 200, 100);
      const particlesGeometry = new THREE.BufferGeometry();
      const particlesCnt = 5000;

      const posArray = new Float32Array(particlesCnt * 3);

      for (let i = 0; i < particlesCnt * 3; i++) {
        //   posArray[i] = Math.random();
        posArray[i] = (Math.random() - 0.5) * 5;
      }

      particlesGeometry.setAttribute(
        "position",
        new THREE.BufferAttribute(posArray, 3)
      );

      // Materials

      const material = new THREE.PointsMaterial({
        size: 0.003,
      });
      material.color = new THREE.Color(
        "#" + Math.floor(Math.random() * 16777215).toString(16)
      );

      const particlesMaterial = new THREE.PointsMaterial({
        size: 0.01,
        map: star,
        transparent: true,
      });

      // Mesh

      const torusKnot = new THREE.Points(geometry, material);
      // const sphere = new THREE.Points(geometry, material);
      const particlesMesh = new THREE.Points(
        particlesGeometry,
        particlesMaterial
      );
      scene.add(particlesMesh);
      scene.add(torusKnot);
      // Lights

      const pointLight = new THREE.PointLight(0xffffff, 0.1);
      pointLight.position.x = 2;
      pointLight.position.y = 3;
      pointLight.position.z = 4;
      scene.add(pointLight);

      /**
       * Sizes
       */
      const sizes = {
        width: window.innerWidth,
        height: window.innerHeight,
      };

      window.addEventListener("resize", () => {
        // Update sizes
        sizes.width = window.innerWidth;
        sizes.height = window.innerHeight;

        // Update camera
        camera.aspect = sizes.width / sizes.height;
        camera.updateProjectionMatrix();

        // Update renderer
        renderer.setSize(sizes.width, sizes.height);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      });

      /**
       * Camera
       */
      // Base camera
      const camera = new THREE.PerspectiveCamera(
        75,
        sizes.width / sizes.height,
        0.1,
        100
      );
      camera.position.x = 0;
      camera.position.y = -0.2;
      camera.position.z = 2.7;
      scene.add(camera);

      // Controls
      // const controls = new OrbitControls(camera, canvas)
      // controls.enableDamping = true

      /**
       * Renderer
       */
      const renderer = new THREE.WebGLRenderer({
        canvas: canvas,
      });
      renderer.setSize(sizes.width, sizes.height);
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      renderer.setClearColor(new THREE.Color("#080808"), 1);

      //Mouse

      document.addEventListener("mousemove", animateParticles);
      // document.addEventListener("mouseleave", startAutoRotate);

      let mouseX = 0;
      let mouseY = 0;

      function startAutoRotate(event) {
        mouseX = 0;
      }

      function animateParticles(event) {
        mouseY = event.clientY;
        mouseX = event.clientX;
      }

      /**
       * Animate
       */

      const clock = new THREE.Clock();
      let ticks = 0;

      const tick = () => {
        ticks += 1;

        const elapsedTime = clock.getElapsedTime();

        // Update objects
        //   sphere.rotation.y = 0.5 * elapsedTime;

        torusKnot.rotation.y = 0.6 * elapsedTime;
        torusKnot.rotation.x = -0.4 * elapsedTime;
        particlesMesh.rotation.y = -0.004 * elapsedTime;
        particlesMesh.rotation.x = -0.005 * elapsedTime;

        if (mouseX != 0) {
          particlesMesh.rotation.x =
            -particlesMesh.rotation.x - mouseY * 0.00005;
          particlesMesh.rotation.y =
            -particlesMesh.rotation.y - mouseX * 0.00005;
        }

        if (ticks % 150 == 0) {
          material.color = new THREE.Color(
            "#" + Math.floor(Math.random() * 16777215).toString(16)
          );
          ticks = 0;
        }

        // Update Orbital Controls
        // controls.update()

        // Render
        renderer.render(scene, camera);

        // Call tick again on the next frame
        window.requestAnimationFrame(tick);
      };

      tick();
    },
  },
  mounted() {
    this.init();
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

html,
body {
  height: 100vh;
  font-family: "Work Sans", sans-serif;
  color: aliceblue;
  overflow-y: auto;
}

.webgl {
  position: fixed;
  top: 0;
  left: 0;
  outline: none;
}

.container {
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 100vh;
  display: grid;
  place-content: center;
}

.content {
  opacity: 0.9;
  width: 100%;
  padding-top: 70vh;
  position: relative;
  text-align: center;
}

/*
  https://developer.mozilla.org/en/docs/Web/CSS/box-shadow
  box-shadow: [inset?] [top] [left] [blur] [size] [color];

  Tips:
    - We're setting all the blurs to 0 since we want a solid fill.
    - Add the inset keyword so the box-shadow is on the inside of the element
    - Animating the inset shadow on hover looks like the element is filling in from whatever side you specify ([top] and [left] accept negative values to become [bottom] and [right])
    - Multiple shadows can be stacked
    - If you're animating multiple shadows, be sure to keep the same number of shadows so the animation is smooth. Otherwise, you'll get something choppy.
*/

// Animate the size, inside
.fill:hover,
.fill:focus {
  box-shadow: inset 0 0 0 2em var(--hover);
}

// Animate the size, outside
.pulse:hover,
.pulse:focus {
  animation: pulse 1s;
  box-shadow: 0 0 0 2em rgba(#fff, 0);
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 var(--hover);
  }
}

// Stack multiple shadows, one from the left, the other from the right
.close:hover,
.close:focus {
  box-shadow: inset -3.5em 0 0 0 var(--hover), inset 3.5em 0 0 0 var(--hover);
}

// Size can also be negative; see how it's smaller than the element
.raise:hover,
.raise:focus {
  box-shadow: 0 0.5em 0.5em -0.4em var(--hover);
  transform: translateY(-0.25em);
}

// Animating from the bottom
.up:hover,
.up:focus {
  box-shadow: inset 0 -3.25em 0 0 var(--hover);
}

// And from the left
.slide:hover,
.slide:focus {
  box-shadow: inset 6.5em 0 0 0 var(--hover);
}

// Multiple shadows, one on the outside, another on the inside
.offset {
  box-shadow: 0.3em 0.3em 0 0 var(--color), inset 0.3em 0.3em 0 0 var(--color);

  &:hover,
  &:focus {
    box-shadow: 0 0 0 0 var(--hover), inset 6em 3.5em 0 0 var(--hover);
  }
}

//=== Set button colors
// If you wonder why use Sass vars or CSS custom properties...
// Make a map with the class names and matching colors
$colors: (
  fill: #a972cb,
  pulse: #ef6eae,
  close: #ff7f82,
  raise: #ffa260,
  up: #e4cb58,
  slide: #8fc866,
  offset: #e7e7e7,
);

// Sass variables compile to a static string; CSS variables are dynamic and inherited
// Loop through the map and set CSS custom properties using Sass variables
@each $button, $color in $colors {
  .#{$button} {
    --color: #{$color};
    --hover: #{adjust-hue($color, 45deg)};
  }
}

// Now every button will have different colors as set above. We get to use the same structure, only changing the custom properties.
button {
  color: var(--color);
  transition: 0.25s;

  &:hover,
  &:focus {
    border-color: var(--hover);
    color: rgb(0, 0, 0);
  }
}

// Basic button styles
button {
  background: none;
  border: 2px solid;
  font: inherit;
  line-height: 1;
  margin: 0.5em;
  padding: 1em 2em;
}

h1 {
  font-weight: 600;
}

code {
  color: #e4cb58;
  font: inherit;
}

</style>
