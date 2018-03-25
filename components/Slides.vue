<template>
<div class="slide-main-body"> 

    <img :src="imgsrc" alt="" class="slide-image">

    <div class="slide-body">

        <h1>{{ slide.title.rendered }}</h1>

        <button>{{imgsrcs}}</button>

    </div>
</div>
</template>

<script>
export default {
    props : ['slide','imgsrcs'],
    data(){
        return{
            imgsrc : "http://powerupboston.com/dev/wp-content/uploads/2016/04/printers02.jpg",
        }
    },
   
};
</script>

<style scoped>
    .slide-image{
       height: 800px;
       max-width: 100%;
       width: 100%;
    }


    .slide-body{
        position: absolute;
        top:50%;
        left:0;
        width: 100%;
        height: 100%;
        text-align: center;
    }

    .slide-main-body{
        position: relative;
        width: 100%;
        height: 100%;
        object-fit: contain;
    }
</style>
