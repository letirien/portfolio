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
        this.$router.push({ path: "/projects", replace: true });
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
.intros {
  min-height: 40vh
}
.intro {
  font-size: 8vw;
  line-height: inherit;
}

.main {
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

</style>
