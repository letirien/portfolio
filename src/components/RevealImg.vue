<template>
    <div class="container-img" :style=style >
        <img src="../assets/Stras.jpg" :class="{'appear': reveal}" alt="cathedrale de Strasbourg" v-if="type ==='head'">
        <img :src="imageSrc" :class="[( revealOther ? 'appear' : '')]"  v-else />
    </div>
</template>

<script>
    export default {
        name: "RevealImg",
        data() {
            return {
                reveal: false,
                revealOther: false,
            };
        },
        props:{
            imageSrc: {
                type: String,
                required: true,
            },
            type: {
                type: String,
                required: false,
            },
            style: String,
        },
        mounted() {
            // Reveal the image on initial load
            setTimeout(()=>{
                this.reveal = true;
            },300)


            // Set up Intersection Observer to reveal subsequent images on scroll
            const options = {
            threshold: 0,
            };

            const observer = new IntersectionObserver((entries, observer) => {
            entries.forEach((entry) => {
                if (entry.intersectionRatio > 0 ) {
                setTimeout(()=>{
                    this.revealOther = true;
                },300)
                    observer.unobserve(entry.target);
                }
            });
            }, options);

            observer.observe(this.$el);
        },
        methods:{
        },

    }
</script>
<style scoped lang="scss">
.container-img{
    position: relative; 
    z-index: -1;
    overflow: hidden;

    img{
        transition: transform 0.5s;
        object-fit: cover;
        width: 100%;
        height: 100%;
        transform: translateY(100%);
        
        &.appear{
        
            transform: translateY(0%);
        }
    }


}
    
</style>