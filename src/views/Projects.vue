<template>
  <div>
    <h1 ref="underline" class="title">Projects</h1>
    <div class="flex">
      <img class="building" src="../assets/work-in-progress.png" alt="" />
    </div>
    <div class="top-24">
      <h2>Voir quelque uns de mes projets :</h2>
      <ul>
        <li :key="index" v-for="(project, index) in projects">
          <a :href="project.link" target="_blank">{{ project.Name }}</a>
          <ol :v-if="project.description">
            {{
              project.description
            }}
          </ol>
          <ol :v-if="project.Image">
            <a
              :href="Img.url"
              :key="Img"
              v-for="Img in project.Image"
              target="_blank"
            >
              {{ Img.name }} /&nbsp
            </a>
          </ol>
        </li>
      </ul>
      <hr />
      <h2 class="top-24">Bonus</h2>
      <ul>
        <li :key="index" v-for="(aussi, index) in also">
          <a :href="aussi.link" target="_blank">{{ aussi.Name }}</a>
          <ol :v-if="aussi.description">
            {{
              aussi.description
            }}
          </ol>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
export default {
  name: "Projects",
  setup() {
    // make users variable reactive with the ref() function
    const projects = ref([
      { Name: "Jiboiana", link: "https://association-jiboiana.com/" },
      { Name: "WowNews Website", link: "https://www.wow-news.eu/" },
      { Name: "WowNews App", link: "https://app.wow-news.eu/" },
      {
        Name: "Plugins Figma",
        Image: [
          {
            id: "attF72OysDsPJcukP",
            name: "insertion d'avatar",
            width: 588,
            height: 644,
            url: "https://dl.airtable.com/.attachments/022ebe8d05c2010da644c6b3d2ef643c/5424414f/image.png",
            filename: "image.png",
            size: 17931,
            type: "image/png",
            thumbnails: {
              small: {
                url: "https://dl.airtable.com/.attachmentThumbnails/26febf3d9e534b4ab52b7b304b15a0f3/de68190c",
                width: 33,
                height: 36,
              },
              large: {
                url: "https://dl.airtable.com/.attachmentThumbnails/6d43c643e8ee0ab0f04b1da733a394c1/59cd9603",
                width: 512,
                height: 561,
              },
              full: {
                url: "https://dl.airtable.com/.attachmentThumbnails/7efa850296e82a5bc3bb7f664b1e675f/c9dfb19e",
                width: 3000,
                height: 3000,
              },
            },
          },
          {
            id: "attAx8GJnnju7eTkW",
            name: "insertion d'avatar 2",
            width: 597,
            height: 664,
            url: "https://dl.airtable.com/.attachments/72d0ee90c5d89baf5b6cd463ef3479c5/93761fad/image.png",
            filename: "image.png",
            size: 34991,
            type: "image/png",
            thumbnails: {
              small: {
                url: "https://dl.airtable.com/.attachmentThumbnails/98e5769686f58be01271aa3c78257561/137e8b83",
                width: 32,
                height: 36,
              },
              large: {
                url: "https://dl.airtable.com/.attachmentThumbnails/6dd9a732b9d6aadcb59eaa950f12a190/6b23c435",
                width: 512,
                height: 569,
              },
              full: {
                url: "https://dl.airtable.com/.attachmentThumbnails/029e86953ba70de3e77be4e143c5eb61/ad05b60e",
                width: 3000,
                height: 3000,
              },
            },
          },
          {
            id: "attiGQjDFvf1W9LTV",
            name: "Frame into Mockup",
            width: 726,
            height: 507,
            url: "https://dl.airtable.com/.attachments/89d229b2097dafb8ece2f6aee7ef9087/b9db5ab4/image.png",
            filename: "image.png",
            size: 206250,
            type: "image/png",
            thumbnails: {
              small: {
                url: "https://dl.airtable.com/.attachmentThumbnails/e431f64d8597a6d28a40862bb7375e97/a9353fcc",
                width: 52,
                height: 36,
              },
              large: {
                url: "https://dl.airtable.com/.attachmentThumbnails/f0cb7ee990ee8a2e78b73c7f650fa3f4/5eb9dcb7",
                width: 726,
                height: 507,
              },
              full: {
                url: "https://dl.airtable.com/.attachmentThumbnails/51d64bf27706aeafca0e6e3fedb389ef/0be6a894",
                width: 3000,
                height: 3000,
              },
            },
          },
        ],
      },
    ]);
    const also = ref([
      {
        link: "https://rentli.fr/",
        Name: "Rentli",
        description:
          "Refonte graphique du site / couleurs / assets / nouvelle page etc",
      },
      {
        link: "https://www.bootnow.co/",
        Name: "Bootnow - Ancienne Alternance",
      },
      {
        link: "https://sprint.studio-uni.fr/",
        Name: "Test d'entrée pour ma première alternance",
      },
    ]);

    return {
      projects,
      also,
    };
  },
  mounted() {
    this.callUnderline();
  },
  created() {
    console.log("Icon made by Pixel perfect from www.flaticon.com");
    this.$nextTick(() => {
      //this.borderEffect();
    });
  },

  methods: {
    callUnderline() {
      let line = this.$refs.underline;

      function underline() {
        line.classList.add("underline");
      }

      setTimeout(underline, 200);
    },

    borderEffect() {
      const main = document.querySelector(".main");
      setTimeout(() => {
        main.classList.add("border");
      }, 400);
    },
  },
};
</script>
<style lang="scss" scoped>
.building {
  max-width: 100%;
  margin: 0 auto;
  transform-origin: top center; // same way can use two keywords
  transform: rotate(-25deg);
  animation: stickUpDown 3s ease-in-out 0s infinite alternate;
}
@keyframes stickUpDown {
  from {
    transform: rotate(-25deg);
  }
  to {
    transform: rotate(25deg);
  }
}
.project_grid {
  height: 576px;
  width: 100%;
}
</style>
