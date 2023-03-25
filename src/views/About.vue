<template>
<div>
  <div class="info">Page en cours de construction</div>
  <header ref="head">
    <div class="normalWrap">
      <div class="headnav flex">
        <h1 ref="underline" class="title">Moi</h1>
        <!-- <router-link to="/about" class="link" @click="callUnderline($event)" @mouseover="(this.scaleDown = true)">A propos de moi</router-link> -->
      </div>
      <div class="head-content">
          <h1 class="intro">Titien SCHOTT</h1>
          <h2 class="intro">Développeur Web</h2>
          <p>From Strasbourg</p>

      </div>
      <RevealImg style="right: 10%; width: 30%; top: 24px;"/>
    </div>
  </header>
  <main class="normalWrap" v-show="false">
    <section >
    </section>
  </main>
  <footer class="normalWrap" v-show="false">
  </footer>
</div>
</template>

<script>
import RevealImg from '../components/RevealImg.vue';
export default {
    name: "About",
    data(){
      return {

      }
    },
    components: [RevealImg],
    mounted() {
        this.callUnderline();
        this.borderEffect();
        this.oberserver()
    },
    methods: {
      oberserver(){
        const observer = new IntersectionObserver(entries => {
          entries.forEach(entry => {
          })
        })
        const El = document.querySelectorAll('.observe');
        El.forEach((el) => {
          observer.observe(el);
        })
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
.info{
  position: fixed;
  padding: 6px;
    height: 34px;
    width: 100%;
    bottom: 0;
    left: 0;
    background: #483f34;
    text-align: center;
    color: white;
}
section{
  padding: 100px 0;
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
}

</style>
