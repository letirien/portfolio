<template>
    <div class="container-img" :style=style ref="container">
        <img src="../assets/Stras.jpg" alt="cathedrale de Strasbourg">
    </div>
</template>

<script>
    export default {
        name: "RevealImg",
        props:{
            content: {
                type: String,
                required: true
            },
            style: String,
        },
        created(){
        setTimeout(() => {
            this.$refs.container.classList.add('appear')
        }, 300);
        }

    }
</script>
<style scoped lang="scss">
.container-img{
    position: absolute; 
    z-index: -1;
    overflow: hidden;

    img{
        transition: 0.5s;
        object-fit: cover;
        width: 100%;
        height: 100%;
        transform: translateY(100%);
    }

    &.appear{
        img{
            transform: translateY(0%);
        }

    }

}
    
</style>