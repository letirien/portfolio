<template>
  <div>
    <div class="normalWrap">
      <h1 ref="underline" class="title">Projects</h1>
    </div>
    <div class="top-24 parent_card_grid">
      <div class="card_grid">
        {{ focus }}
        <ProjectCard :id="project.Name" class="kid" :focus='!isMobile? firstEl: ""' :key="index"
                     v-for="(project, index) in projects" :content="project"/>
      </div>
    </div>
    <div class="normalWrap foot">
      <div class="nav_projects" v-show="!isMobile">
        <p @click="scroll($event)" class="h2 project_link" :id="'link'+project.Name" :class="project.Name==='Jiboiana'?'underline': ''"
           v-for="(project, index) in clone ">{{ project.Name }}</p>
      </div>
      <div class="arrowParent" v-show="!isMobile">
        <div class="stickmanWalking" v-if="this.slide"
             :style="this.right? '': 'transform: translateX(-50%) rotateY(180deg); right: -78px'"><img
            src="../assets/walking.gif" alt=""></div>
        <div class="stickman" v-else :style="this.right? '': 'transform: translateX(-50%) rotateY(180deg);'"><img
            src="../assets/notWalking.png" alt=""></div>
        <svg @click="go('left')" class="arrow left" width="59" height="24" viewBox="0 0 59 24" fill="none"
             xmlns="http://www.w3.org/2000/svg">
          <path
              d="M0.93934 10.9393C0.353553 11.5251 0.353553 12.4749 0.93934 13.0607L10.4853 22.6066C11.0711 23.1924 12.0208 23.1924 12.6066 22.6066C13.1924 22.0208 13.1924 21.0711 12.6066 20.4853L4.12132 12L12.6066 3.51471C13.1924 2.92893 13.1924 1.97918 12.6066 1.39339C12.0208 0.807608 11.0711 0.807608 10.4853 1.39339L0.93934 10.9393ZM59 10.5L2 10.5L2 13.5L59 13.5L59 10.5Z"
              fill="black"/>
        </svg>
        <svg @click="go('right')" class="arrow right" width="59" height="24" viewBox="0 0 59 24" fill="none"
             xmlns="http://www.w3.org/2000/svg">
          <path
              d="M58.0607 13.0607C58.6464 12.4749 58.6464 11.5251 58.0607 10.9393L48.5147 1.3934C47.9289 0.807616 46.9792 0.807616 46.3934 1.3934C45.8076 1.97919 45.8076 2.92894 46.3934 3.51472L54.8787 12L46.3934 20.4853C45.8076 21.0711 45.8076 22.0208 46.3934 22.6066C46.9792 23.1924 47.9289 23.1924 48.5147 22.6066L58.0607 13.0607ZM-1.31134e-07 13.5L57 13.5L57 10.5L1.31134e-07 10.5L-1.31134e-07 13.5Z"
              fill="black"/>
        </svg>

      </div>
    </div>
    <svg class="slideHand" width="60" height="60" viewBox="0 0 437 306" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect x="203" y="43" width="13" height="151" fill="black"/>
      <rect x="241" y="42" width="13" height="151" fill="black"/>
      <rect x="353" y="143" width="13" height="88" fill="black"/>
      <rect x="341" y="231" width="13" height="38" fill="black"/>
      <rect x="328" y="268" width="13" height="38" fill="black"/>
      <rect x="316" y="131" width="13" height="38" fill="black"/>
      <rect x="278" y="118" width="13" height="38" fill="black"/>
      <rect x="216" y="268" width="13" height="38" fill="black"/>
      <rect x="203" y="243" width="13" height="25" fill="black"/>
      <rect x="191" y="217" width="13" height="26" fill="black"/>
      <rect x="178" y="193" width="13" height="25" fill="black"/>
      <rect x="153" y="156" width="13" height="25" fill="black"/>
      <rect x="216" y="30" width="25" height="13" fill="black"/>
      <rect x="254" y="93" width="25" height="13" fill="black"/>
      <rect x="316" y="118" width="25" height="13" fill="black"/>
      <rect x="341" y="130" width="13" height="13" fill="black"/>
      <rect x="190" y="156" width="13" height="13" fill="black"/>
      <rect x="166" y="180" width="13" height="13" fill="black"/>
      <rect x="278" y="105" width="38" height="13" fill="black"/>
      <rect x="153" y="143" width="38" height="13" fill="black"/>
      <rect x="229" y="293" width="99" height="13" fill="black"/>
      <path d="M435.828 32.8284C437.391 31.2663 437.391 28.7337 435.828 27.1716L410.373 1.71573C408.81 0.153632 406.278 0.153632 404.716 1.71573C403.154 3.27783 403.154 5.81049 404.716 7.37258L427.343 30L404.716 52.6274C403.154 54.1895 403.154 56.7222 404.716 58.2843C406.278 59.8464 408.81 59.8464 410.373 58.2843L435.828 32.8284ZM291 34H433V26H291V34Z" fill="black"/>
      <path d="M1.17157 27.1716C-0.390524 28.7337 -0.390524 31.2663 1.17157 32.8284L26.6274 58.2843C28.1895 59.8464 30.7222 59.8464 32.2843 58.2843C33.8464 56.7222 33.8464 54.1895 32.2843 52.6274L9.65685 30L32.2843 7.37257C33.8464 5.81048 33.8464 3.27782 32.2843 1.71572C30.7222 0.153621 28.1895 0.153621 26.6274 1.71572L1.17157 27.1716ZM153 26L4 26L4 34L153 34L153 26Z" fill="black"/>
    </svg>

  </div>
</template>
<script>
import {ref} from "vue";
import ProjectCard from "../components/ProjectCard.vue";

export default {
  name: "Projects",
  components: {ProjectCard},
  setup() {
    // make users variable reactive with the ref() function
    const projects = ref([]);
    const clone = ref([])
    const firstEl = ref('');
    const clickCount = ref(0)
    let right = ref(true)
    let current = ref(0)
    let old = ref(null)
    const slide = ref(false);

    fetch("https://api.airtable.com/v0/appTE72qZSTNVsNrL/projects?maxRecords=100&view=Grid%20view", {
      headers: {
        'Content-type': 'application/json',
        'Authorization': `Bearer key9a1KxVxfytXi0P`, // notice the Bearer before your token
      },

    })
        .then((response) => response.json())
        .then((data) => {
          firstEl.value = data.records[0].fields.Name
          data.records.map(e => {
            projects.value.push(e.fields)
            clone.value.push(e.fields)

          })
        })

    return {
      projects,
      firstEl,
      clone,
      right,
      current,
      old,
      slide,
      clickCount,
    }
  },
  computed: {
    isMobile() {
      return window.matchMedia('only screen and (max-width: 768px)').matches;
    }
  },
  mounted() {
    this.callUnderline();
    const wrap = document.querySelector('.normalWrap')
    const parentGrid = document.querySelector('.parent_card_grid')
    const padding = parseInt(window.getComputedStyle(wrap, null).getPropertyValue('padding-left'))
    parentGrid.style.marginLeft = (wrap.offsetLeft + padding) + 'px'
    window.addEventListener('resize', () => {
      parentGrid.style.marginLeft = (wrap.offsetLeft + padding)  + 'px'
    });
  },
  created() {
    const container = window.document.querySelector('.container')
    container.classList.contains("wrap") ? container.classList.remove('wrap'): ''
  },
  methods: {
    walk() {
      this.slide = true
    },
    stop() {
      this.slide = false
    },
    changeDirection(elClicked) {
      let indexOfClicked = this.projects.indexOf(this.projects.find(el => el.Name === elClicked))
      if (this.current === null) {
        this.current = indexOfClicked
      } else {
        this.old = this.current
        this.current = indexOfClicked
      }

      if (this.old < this.current) {
        this.right = true
      } else {
        this.right = false
      }

    },
    go(direction) {
      this.current ? this.clickCount = this.current: ''
        if (direction === 'right') {
          if (this.clickCount < this.projects.length -1) {
            this.clickCount += 1
          }
        } else {
          if (this.clickCount > 0) {
            this.clickCount -= 1
          }
        }
        const elInArray = this.projects[this.clickCount].Name
        const elToClick = document.getElementById('link'+elInArray)
        elToClick.click()
    },
    scroll(e) {
      if (!this.isMobile) {
        this.walk()
        setTimeout(this.stop, 200)
        let view = document.getElementById(e.target.textContent)
        this.firstEl = view.id
        const parent = document.querySelector('.card_grid')
        const card = document.querySelectorAll('.card')
        let scrollNeeded = view.offsetLeft - parent.offsetLeft
        card.forEach((el) => {
          el.style.transform = "translateX(-" + scrollNeeded + "px)"
        })
        document.querySelectorAll('.project_link').forEach(el => {
          if (el.getElementsByClassName('underline')) {
            el.classList.remove('underline')
          }
          e.target.classList.add('underline')
        })
        this.changeDirection(e.target.textContent)
      }

    },
    callUnderline() {
      let line = this.$refs.underline;

      function underline() {
        line.classList.add("underline");
      }

      setTimeout(underline, 200);
    },

  },
};
</script>
<style lang="scss" scoped>
@media (max-width: 768px) {
  .slideHand{
    display: block!important;
    position: absolute;
    right: 24px;
    top: 24px;
  }
  .foot {
    display: none!important;
  }
    /* ??? */
  .card_grid {
    padding-top: 0px !important;
    grid-auto-columns: auto !important;
    grid-column-gap: 48px !important;
    scroll-snap-type: x mandatory;
    -ms-scroll-snap-type: x mandatory;
    scroll-behavior: smooth;
    overflow-x: scroll !important;

    .kid {
      scroll-snap-align: start;
    }

  }

  .card_grid::-webkit-scrollbar-track {
    background-color: transparent;
  }

  .card_grid::-webkit-scrollbar {
    height: 6px;
    background-color: transparent;
  }

  .card_grid::-webkit-scrollbar-thumb {
    background-color: black;
    position: relative;

    &:after{
      content: '>';
      position: absolute;
      width: 8px;
      height: 6px;
      background: red;
    }
  }

}
.slideHand{
  display: none;
}
.card_grid {
  padding-top: 50px;
  display: grid;
  grid-auto-columns: 464px;
  grid-column-gap: 160px;
  grid-auto-flow: column;
  scroll-snap-type: x mandatory;
  -ms-scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
  overflow-x: hidden;
}

.foot {
  align-items: flex-end;
  height: 150px;
  position: absolute;
  bottom: 48px;
  display: flex;
  justify-content: space-between;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  overflow: hidden;

  .arrowParent {
    -webkit-user-select: none; /* Safari */
    -ms-user-select: none; /* IE 10 and IE 11 */
    user-select: none; /* Standard syntax */
    .arrow {
      width: 80px;
      position: relative;
      cursor: pointer;

      &.left {
        margin-right: 4px;
      }

      &.right {
        margin-left: 4px;
      }
    }

    .stickman {
      width: 80px;
      position: absolute;
      top: 15px;
      right: 24px;
      transform: translateX(-50%);

      img {
        width: 100%;
      }
    }

    .stickmanWalking {
      height: 165px;
      position: absolute;
      top: -7px;
      right: -107px;
      transform: translateX(-50%);

      img {
        width: 100%;
        height: 100%;
      }
    }
  }

}

.nav_projects {
  max-width: 65%;

  .project_link {
    cursor: pointer;
    margin-right: 32px;
  }
}


</style>
