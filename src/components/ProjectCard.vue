<script>

    import { store } from '../store.js';

    export default{
        name:'ProjectCard',
        props:['project'],
        data() {
            return {
                store
            }
        }
    }
</script>

<template>
    <div class="card bg-black text-white text-center">
        <img v-if="project.cover_image" :src="`${this.store.url}/storage/${project.cover_image}`" class="card-img-top" :alt="project.title"/>
        <img v-else src="https://picsum.photos/200/200" class="card-img-top" :alt="project.title"/>
        <div class="card-body card-wrapper">
            <h5 class="card-title py-3">{{project.title}}</h5>
            <div v-if="project.tecnologies" class="d-flex justify-content-center flex-wrap">
                <p class="pe-2 badge text-bg-primary" v-for="tecnology in project.tecnologies">{{tecnology.name_tech}}</p>
            </div>
            <p class="card-text">{{project.content}}</p>
            <p class="badge text-bg-primary">{{project.type?.name}}</p>
            <router-link :to="{name: 'single-project', params: {slug: project.slug}}" class="btn btn-primary">
                Vedi project completo
            </router-link>

        </div>
    </div>
</template>

<style scoped lang="scss">
    .card-wrapper{
        height: 350px;
    }
    
</style>