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
            });

        }
    }
</script>

<template>
    <h1>Singolo Project</h1>
</template>