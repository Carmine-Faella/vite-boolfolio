<script>
  import axios from 'axios';
  import ProjectCard from './ProjectCard.vue';

export default {
    name: 'AppMain',
    components: {
            ProjectCard,
    },
    data() {
        return {
            projects: [],
            url: 'http://localhost:8000',
            currentPage: 1,
            lastPage: null
        }
    },
    methods: {
        getProjects(gotoPage) {

            axios.get(`${this.url}/api/projects`,
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
            <ProjectCard 
                :image="projects.cover_image" 
                :url="this.url" 
                :title="project.title" 
                :content="project.content"
                :type="project.type"
                :tecnologies="project.tecnologies">
            </ProjectCard>
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