<script>
    import axios from 'axios';
    import { store } from '../store.js';

    export default {
        name: 'SinglePost',
        data() {
            return {
                store
            }
        },
        mounted() {
            const slug = this.$route.params.slug;
            
            console.log(slug);

            axios.get(`${this.store.url}/api/project/${slug}`)
            .then(response => {
                console.log(response);
                this.project = response.data.results;
            });

        }
    }
</script>

<template>
    <div class="text-center">
        <h1>{{ project.title }}</h1>
        <div class="py-3">{{ project.content }}</div>
        <div v-if="project.tecnologies" class="d-flex justify-content-center flex-wrap">
            <p class="pe-2 badge text-bg-primary" v-for="tecnology in project.tecnologies">{{tecnology.name_tech}}</p>
        </div>
        <div v-if="project.type">{{project.type.name}}</div>
    </div>

</template>