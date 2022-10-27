<template>
<div class="card" :class="focus === content.Name ? '': focus === '' ? '': 'small'">
    <div class="cardHead flex justify-between">
      <h2>{{content.Name}}</h2>
      <div class="tags">
        <p v-for="tag in content.Tags">#{{tag}} &nbsp </p>
      </div>
    </div>
    <div class="cardBody">
      <div class="container-img">
        <img :src="content.Image[0].url" alt="">
      </div>
      <p :style="focus === content.Name? '': focus ===''? 'opacity: 1': 'opacity: 0'">
        {{ content.description }}
      </p>
    </div>
    <div class="cardFooter" :style="focus === content.Name?'': focus===''? 'opacity: 1': 'opacity: 0'">
      <div class="link">
        <a :href="content.link">Voir le site</a>
        <svg width="57" height="16" viewBox="0 0 57 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M56.7071 8.70711C57.0976 8.31658 57.0976 7.68342 56.7071 7.29289L50.3431 0.928932C49.9526 0.538408 49.3195 0.538408 48.9289 0.928932C48.5384 1.31946 48.5384 1.95262 48.9289 2.34315L54.5858 8L48.9289 13.6569C48.5384 14.0474 48.5384 14.6805 48.9289 15.0711C49.3195 15.4616 49.9526 15.4616 50.3431 15.0711L56.7071 8.70711ZM0 9H56V7H0V9Z" fill="black"/>
        </svg>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProjectCard",
  props:{
    content: {},
    focus: String,

  },
  computed:{
    isMobile(){
      return window.matchMedia('only screen and (max-width: 768px)').matches;
    }
  },
}
</script>

<style scoped lang="scss">
@media (max-width: 768px) {
  .card {
    height: fit-content;
    padding: 16px!important;
    width: calc(100vw - 36px);
  }
  .cardBody {
    .container-img {
      p {
        opacity: 1 !important;
      }
    }
  }
}
.card{
  position:relative;
  //max-height: 100%;
  max-width: 464px;
  background: white;
  padding: 24px;
  border: 3px solid black;
  transition: transform 0.4s cubic-bezier(0.45, 0.05, 0.55, 0.95), max-height 0.1s linear 0.05s  ;
  .cardHead{
    align-items: center;
    margin-bottom: 24px;
    .tags{
      display: flex;
      flex-wrap: wrap;
      max-width: 50%;
      justify-content: end;
    }
  }
  .cardBody{
    .container-img{
      width:100%;
      height: 200px;
      margin-bottom: 24px;
      filter: drop-shadow(0px 0px 4px rgba(0, 0, 0, 0.6));

      img{
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: top;
      }
    }
    p{
      transition: opacity linear 0.4s;
    }
  }

  .cardFooter{
    transition: opacity linear 0.4s;
    margin-top: 24px;
    display: flex;
    justify-content: flex-end;
    .link{
      width: 70px;
      display: flex;
      flex-direction: column;
      align-items: center;

      svg{
        margin-top: 4px;
        transition: ease 0.2s;
      }
      &:hover svg{
        transform: translateX(4px);

      }
    }
  }
  &.small{
    max-height: 319px;
    overflow: hidden;

  }

}
/*.card.focused{
    :after{
      position: absolute;
      content:'';
      width: 50%;
      height: 3px;
      bottom: -6px;
      left: 0;
      background: black;

    }
}


 */

</style>
