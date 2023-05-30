<script>

    export default{
        name:'ProjectCard',
        props:{
            image:String,
            url:String,
            title:String,
            content:String
        }
    }
</script>

<template>
    <div class="card bg-black text-white text-center">
        <img v-if="image" :src="`${url}/storage/${image}`" class="card-img-top" :alt="title"/>
        <img v-else src="https://picsum.photos/200/200" class="card-img-top" :alt="title"/>
        <div class="card-body card-wrapper">
            <h5 class="card-title py-3">{{title}}</h5>
            <p class="card-text">{{content}}</p>
            <a href="#" class="btn btn-primary mt-3">Vedi project completo</a>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .card-wrapper{
        height: 300px;
    }
    
</style>