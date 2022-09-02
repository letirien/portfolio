<template>
  <div>
    <div data-scroll>
      <h1 ref="underline" class="title">Portfolio</h1>
      <main class="main">
        <div class="intros">
          <p class="intro">Bonjour</p>
          <p class="intro">Bienvenue</p>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
  components: {},
  data() {
    return {};
  },
  mounted() {
    this.show = true; // might need this.$nextTick
    this.callUnderline();
  },
  created() {
    this.$nextTick(() => {
      this.borderEffect();
      setTimeout(() => {
        //this.$router.push({ path: "/projects", replace: true });
      }, 2000);
    });
  },
  methods: {
    borderEffect() {
      const main = document.querySelector(".main");
      setTimeout(() => {
        main.classList.add("border");
      }, 400);
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
@media screen and (max-width: 1024px) {
  .intro {
    font-size: 164px !important;
  }
}
@media screen and (max-width: 768px) {
  .intro {
    font-size: 86px !important;
  }
}
@media screen and (max-width: 512px) {
  .intro {
    font-size: 64px !important;
  }
}
@media screen and (max-width: 375px) {
  .intro {
    font-size: 48px !important;
  }
}
.intros {
  height: 576px;
}
.intro {
  font-size: 180px;
}
canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
  pointer-events: none;
}

/* Page Loader */
.js .loading::before,
.js .loading::after {
  content: "";
  position: fixed;
  z-index: 1000;
}

.js .loading::before {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--color-bg);
}

.js .loading::after {
  top: 50%;
  left: 50%;
  width: 60px;
  height: 60px;
  margin: -30px 0 0 -30px;
  border-radius: 50%;
  opacity: 0.4;
  background: var(--color-link);
  animation: loaderAnim 0.7s linear infinite alternate forwards;
}

@keyframes loaderAnim {
  to {
    opacity: 1;
    transform: scale3d(0.5, 0.5, 1);
  }
}

.appear-enter-active {
  transition: opacity 0.5s ease-in;
}

.appear-enter {
  opacity: 0;
}

.me {
  width: 450px;
}
</style>
