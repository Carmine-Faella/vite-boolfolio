<script>
    import axios from 'axios';
    import { store } from '../store.js';

    export default {
        name: 'SingleProject',
        data() {
            return {
                store,
                projects:null
            }
        },
        mounted() {
            const slug = this.$route.params.slug;
            
            axios.get(`${this.store.url}/api/projects/${slug}`)
            .then(response => {
                if(response.data.success == true){
                    this.projects = response.data.results;
                }else{
                    this.$router.push({name:'NotFound'});
                }
                console.log(this.projects)
                console.log(response.data)
            });

        }
    }
</script>

<template>

    <div v-if="projects" class="text-center">
        <div class="pb-3">
            <img v-if="projects.cover_image" :src="`${this.store.url}/storage/${projects.cover_image}`" class="img-fluid" :alt="projects.title"/>
            <img v-else src="https://picsum.photos/300" class="img-fluid text-center" :alt="projects.title"/>   
        </div>
        
        <h5 class="">{{projects.title}}</h5>
        <div v-if="projects.tecnologies" class="d-flex justify-content-center">
            <div class="pe-2 my-3 badge text-bg-primary" v-for="tecnology in projects.tecnologies">{{tecnology.name_tech}}</div>
        </div>
        <div class="badge text-bg-primary">{{projects.type?.name}}</div>
        <p>{{projects.content}}</p>

    </div>

</template>
