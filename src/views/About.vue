<template>
<div id="scroll-container">
  <div class="info">Page en cours de construction <p>RESPONSIVE NOT READY</p></div>
  <header ref="head">
    <div class="normalWrap">
      <div class="headnav flex">
        <h1 ref="underline" class="title">Moi</h1>
        <!-- <router-link to="/about" class="link" @click="callUnderline($event)" @mouseover="(this.scaleDown = true)">A propos de moi</router-link> -->
      </div>
      <div class="head-content">
          <h1 class="intro">Titien<br> SCHOTT</h1>
          <h2 class="intro">Développeur Web</h2>
          <p>From Strasbourg</p>

      </div>
      <div id="canvas" class="head-img"/>
    </div>
  </header>
  <main class="normalWrap">
        <section class="dev">
          <div class="flex-text right">
            <div>
            <H2 class="">Développement Web</H2>
            <div >
              <p class="p1" >Fortement minutieux au rendu visuel, je développe des interfaces web avec rigueur et passion. </p>
              <p class="p2">Ma technologie de prélidiction est le framework Vue.js. </p>
              <p class="p3">A l'aise avec le langage Javascript et ayant des bases dans d'autres frameworks et librairies tels que React, Three.js .. je suis capable de m'adapter à différents type de projet et de me former rapidement à l'utilisation de nouveaux outils et technologies.</p>
            </div>
            </div>
            <img src="../assets/beer.png" alt=""  style="margin-right: 24px; width:40%">
          </div>
        </section>
        <section class="about-me-sec" id="sticky-sec">
          <div class="flex-text">
            <div class="text">
              <H2>A PROPOS DE MOI</H2>
              <div>
                <p class="p1" >Née à Strasbourg en 99, de peu d'être un 2000, mon parcour de vie m'a mené jusqu'au développement front-end,  </p>
                <p class="p2">J'ai notamment pu étudier à l'IUT de Haguenau, dans un premier temps dans le cadre d'un DUT MMI (Métier du multimédia et de l'internet) et dans un second temps pour une année d'étude supplémentaire dans le cadre d'une License Professionnelle Développement web et
                  conception d'interfaces.
                </p>
                <p>J'évolue depuis maintenant octobre 2021 en tant que jeune freelance, qui rythme sa vie entre passion pour la production musicale et projets web.</p>
              </div>
            </div>
            <div class="me-img">
              <RevealImg  :image-src="getImageUrl(pageImage.me)" style="width: 100%; height: 100%; "/>
              <div class="interaction" v-if="false">
                <div class="container-diag">
                  <p>Ceci est ma photo d'identité</p>
                </div>
                <div class="container-stick">
                  <img src="../assets/notWalking.png" alt="">
                </div>
              </div>
            </div>
          </div>
        </section>
      </main>
  <footer class="normalWrap" v-show="false">
  </footer>
</div>
</template>

<script>
import RevealImg from '../components/RevealImg.vue';
import * as THREE from 'three'
import openSimplexNoise from 'https://cdn.skypack.dev/open-simplex-noise';
import {gsap} from 'gsap'

export default {
    name: "About",
    data(){
      return {
      pageImage: {
        header: 'Stras.jpg',
        me: 'me.jpg'
      },
      scaleDown : false
    };
    },
    components: [RevealImg],
    computed:{
      sphereDeclare(){
      let sphereGeometry = new THREE.SphereGeometry(1.5, 100, 100);
      sphereGeometry.positionData = [];
      let v3 = new THREE.Vector3();
      for (let i = 0; i < sphereGeometry.attributes.position.count; i++){
        v3.fromBufferAttribute(sphereGeometry.attributes.position, i);
        sphereGeometry.positionData.push(v3.clone());
      }
      let sphereMesh = new THREE.MeshStandardMaterial({color: '#f7c548', roughness: 0.2, metalness: 0.3})
      let sphere = new THREE.Mesh(sphereGeometry, sphereMesh);
      const three =  {
        sphere: sphere,
        geometry : sphereGeometry,
        mesh : sphereMesh,
        v3: v3
      }
      return three
      }
  },
    mounted() {
        this.callUnderline();
        this.borderEffect();
        this.obserserver()
        this.THREE()

    },
    methods: {
      THREE() {
      //const raycaster = new THREE.Raycaster();
      const container = document.getElementById('canvas');
      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(45, container.offsetWidth / container.offsetHeight, 0.1, 50);
      camera.position.z = 15;

      const renderer = new THREE.WebGLRenderer({alpha: true});
      renderer.setPixelRatio(window.devicePixelRatio);
      renderer.setSize(container.offsetWidth, container.offsetHeight);
      container.appendChild(renderer.domElement);

      const lights = [];
      lights[0] = new THREE.PointLight(0xffffff, 1, 0);
      lights[1] = new THREE.PointLight(0xffffff, 1, 0);
      lights[2] = new THREE.PointLight(0xffffff, 1, 0);

      lights[0].position.set(0, 200, 0);
      lights[1].position.set(100, 200, 100);
      lights[2].position.set(-100, -200, -100);

      scene.add(lights[0]);
      scene.add(lights[1]);
      scene.add(lights[2]);


      let sphere = this.sphereDeclare.sphere
      let sphereGeometry = this.sphereDeclare.geometry
      let v3 = this.sphereDeclare.v3
      //ici récup this.sphere from computed
      scene.add(sphere);
      const clonePos = sphere.position.clone(sphere)
      //sphere.rotation.x = +45

      let planeGeometry = new THREE.BoxGeometry(7, 7, 2, 10, 10, 2)
        planeGeometry.translate(0, 0, -3);
        planeGeometry.positionData = [];
        for (let i = 0; i < planeGeometry.attributes.position.count; i++){
          v3.fromBufferAttribute(planeGeometry.attributes.position, i);
          planeGeometry.positionData.push(v3.clone());
        }

        let noise = openSimplexNoise.makeNoise4D(Date.now());
        let clock = new THREE.Clock();

        window.addEventListener("resize", () => {
          camera.aspect = innerWidth / innerHeight;
          camera.updateProjectionMatrix();
          renderer.setSize(innerWidth, innerHeight)
        });

        renderer.setAnimationLoop( () => {
          let t = clock.getElapsedTime() / 1.;
          sphereGeometry.positionData.forEach((p, idx) => {
            let setNoise = noise(p.x, p.y, p.z, t * 1.05);
            v3.copy(p).addScaledVector(p, setNoise);
            sphereGeometry.attributes.position.setXYZ(idx, v3.x, v3.y, v3.z);
          })
          sphereGeometry.computeVertexNormals();
          sphereGeometry.attributes.position.needsUpdate = true;

          planeGeometry.positionData.forEach((p, idx) => {
            let setNoise = noise(p.x, p.y, p.z, t / 3);
            v3.copy(p).addScaledVector(p, setNoise);
            planeGeometry.attributes.position.setXYZ(idx, v3.x, v3.y, v3.z);
          })
          planeGeometry.attributes.position.needsUpdate = true;
          renderer.render(scene, camera);
        })

      function render() {
        //update()
        requestAnimationFrame(render);
        renderer.render(scene, camera);
      }
      render();
    },
      obserserver(){
        function debounce(func, wait) {
          let timeout;
          return function() {
            const context = this, args = arguments;
            clearTimeout(timeout);
            timeout = setTimeout(() => {
              timeout = null;
              func.apply(context, args);
            }, wait);
          };
        }
            // Set up Intersection Observer to reveal subsequent images on scroll
        const options = {
          // rootMargin: "200px",
          threshold: 0.1,
        } ;
        const observer = new IntersectionObserver(debounce((entries, observer) => {
          entries.forEach((entry) => {
              const H2 = entry.target.querySelector('.text').firstChild
              const p = entry.target.querySelector('.text').children[1]
              const img = entry.target.querySelector('.me-img')
            if (entries[0].intersectionRatio !== 0) {
              document.querySelector('body').classList.add('darker')
              setTimeout(()=>{
                document.querySelector('body').classList.add('darker')
                img.classList.add('shadow')
                H2.classList.add('appear')
                p.classList.add('appear')
              }, 800)
    
            } else {
              if (document.querySelector('body').classList.contains('darker')) {
                document.querySelector('body').classList.remove('darker')
              }
            }
          })
        },0))
        const myEl = document.querySelector('.about-me-sec');
        observer.observe(myEl, options);
      },
      getImageUrl(el){
        return new URL(`../assets/${el}`, import.meta.url).href
      },
        callUnderline(el) {
            let line;
            el ? line = el.target : line = this.$refs.underline;
            function underline() {
                line.classList.add("underline");
            }
            setTimeout(underline, 200);
        },
        borderEffect() {
            const intro = document.querySelector(".head-content");
            setTimeout(() => {
                intro.classList.add("border");
            }, 400);
        },
    },
    components: { RevealImg }
}
</script>

<style scoped lang="scss">
.head-img canvas{
  width: 100%!important;
}
@media (max-width: 1024px) {
header{
  height: 50vh!important;
}
}
.head-img{
  position: absolute;
  width: 50%;
  right: -10%;
  top: 24px;
  bottom: 0;
  z-index: -5;
}
.about-me-sec{
  margin-top: 80px;
  position: relative;
  width: 100%;
  height: 800px;
  .me-img{
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    bottom: 0;
    width:50% ;
    height: 100%;
    -webkit-filter: grayscale(100%); /* Safari 6.0 - 9.0 */
    filter: grayscale(100%) brightness(90%);
    transition: 0.3s;

    &.shadow{
      -webkit-box-shadow: 0px 0px 100px 24px #000000; box-shadow: 0px 0px 100px 24px #000000;
    }
  }
  .text{
    text-align: center;
    position: absolute;
    top: 0;
    /* left: 50%; */
    /* transform: translateX(-50%); */
    z-index: 2;


    h2{
      margin: 24px 0;
      opacity: 0;
      transition: opacity 0.4s;
      &.appear{
        opacity: 1;
      }

    }
    div{
      opacity: 0;
      transition-delay: 0.7s;
      transition: opacity 0.5s;
      p{
        color: #EBE8D1;

        &::selection {
          color: black;
        }
      }
      &.appear{
        opacity: 1;
      }
    }

  }
}
.info{
  position: fixed;
  z-index: 3;
  padding: 6px;
    width: 100%;
    bottom: 0;
    left: 0;
    background: #483f34;
    text-align: center;
    color: white;
}
section{
  padding: 180px 0;

  .flex-text {
    display: flex;

    h2{
      margin-bottom: 24px;
    }

    p{
      font-size: 18px;
      line-height: 24px;
    }
    &.right {
      flex-direction: row-reverse;

    }
  }
}
.head-content{
  .intro {
    line-height: 1;
    font-style: normal;
    font-weight: 400;
    mix-blend-mode: difference;
    color: white;
    &::selection{
      background: none;
    }
  }
  h1{
    font-size: 7vw;
    margin-bottom: 24px;
  }
  h2{
    font-size: 6vw;
  }
  p{
    font-weight: bold;
    font-size: large;
  }
  margin-top: 20vh;
  position: relative;
  padding-left: 24px;

  &:after {
    position: absolute;
    content: "";
    width: 4px;
    left: 0;
    bottom: 0;
    height: 0%;
    background: black;
    transition: height 0.5s;
  }
  &.border:after {
    width: 4px;
    position: absolute;
    content: "";
    left: 0;
    bottom: 0;
    height: 100%;
    background: black;
    transition: height 0.5s;
  }
  }
header{
  height: calc(100vh - 24px);
  // background: #eeebd3;
  .normalWrap{
    position: relative;
  }
}

</style>
