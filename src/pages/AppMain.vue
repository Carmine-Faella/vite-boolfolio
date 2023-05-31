<script>
  import axios from 'axios';
  import ProjectCard from '../components/ProjectCard.vue';
  import {store} from '../store.js';

export default {
    name: 'AppMain',
    components: {
            ProjectCard,
    },
    data() {
        return {
            projects: [],
            store,
            currentPage: 1,
            lastPage: null
        }
    },
    methods: {
        getProjects(gotoPage) {

            axios.get(`${this.store.url}/api/projects`,
                {
                    params: {
                        page: gotoPage
                    }
                }
            )
            .then(response => {
                console.log(response);
                this.projects = response.data.results.data;
                this.currentPage = response.data.results.current_page;
                this.lastPage = response.data.results.last_page;
            });
        }
    },
    mounted() {
        this.getProjects(1);
    }


}
</script>

<template>

<div class="container">
    <div class="row">

        <div class="col-4" v-for="project,index in projects" :key="index">
            <ProjectCard :project="project"></ProjectCard>
        </div>

        <nav aria-label="Page navigation example">
            <ul class="pagination mt-5 d-flex justify-content-center">
                <li class="page-item"><button class="page-link" @click="getProjects(currentPage - 1)" :class="{'disabled' : currentPage == 1}">Previous</button></li>
                <li class="page-item"><button class="page-link" @click="getProjects(currentPage + 1)" :class="{'disabled' : currentPage == lastPage}">Next</button></li>
            </ul>
        </nav>
    </div>
</div>

  
</template>

<style scoped lang="scss">

</style>