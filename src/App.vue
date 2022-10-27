<template>
    <div :class="$route.path !== '/projects'?  'wrap' : ''">
      <router-view v-slot="{ Component }">
        <transition name="component-fade" mode="out-in" appear>
          <component :is="Component" />
        </transition>
      </router-view>
    </div>
</template>
<script>
export default {};
</script>
<style lang="scss">
@import "src/assets/styles/styles.scss";
@import url("https://fonts.googleapis.com/css2?family=Libre+Baskerville&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&family=Kosugi&display=swap');
.component-fade-enter-active,
.component-fade-leave-active {
  transition: opacity 0.5s ease;
}
.component-fade-enter, .component-fade-leave-to
  /* .component-fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
