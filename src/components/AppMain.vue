<script>
  import axios from 'axios';

export default {
    name: 'AppMain',
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

        <div class="col-4" v-for="project in projects">
            <div class="card bg-black text-white text-center">
                <img v-if="projects.cover_image" :src="`${this.url}/storage/${projects.cover_image}`" class="card-img-top">
                <img v-else src="https://picsum.photos/200/200" class="card-img-top"/>
                <div class="card-body card-wrapper">
                    <h5 class="card-title py-3">{{project.title}}</h5>
                    <p class="card-text">{{project.content}}</p>
                    <a href="#" class="btn btn-primary mt-3">Vedi project completo</a>
                </div>
            </div>
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

    .card-wrapper{
        height: 300px;
    }

</style>