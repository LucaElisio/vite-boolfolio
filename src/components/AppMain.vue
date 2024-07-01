<script>
import axios from 'axios';

import ProjectCard from './ProjectCard.vue';

export default {

    components: {
        ProjectCard
    },

    data() {
        return {
            projects: [],
            lastPage: 0,
            curPage: 1,
        }
    },

    created(){
        this.getProjects()
    },

    methods: {

        getProjects(){
            axios
                .get('http://127.0.0.1:8000/api/projects', {
                    params: {
                        page: this.curPage,
                    },
            })
                .then((resp) => {

            // Prelevo i dati e li assegno a projects
            this.projects = resp.data.result.data;
            this.lastPage = resp.data.result.last_page;

            })
        },

        changePage(newPage){
            this.curPage = newPage;
            this.getProjects();
        },

        nextPage(){
            if(this.curPage < this.lastPage) {
                this.curPage++;
                this.getProjects(); 
            }
        },

        prevPage(){
            if(this.curPage !== 1){
                this.curPage--;
                this.getProjects();
            }
        }
    }
}
</script>

<template>
    <h1>App Main</h1>
    <div class="container">
        <div class="row">
            <div class="col" v-for="project in this.projects">
                <ProjectCard class="h-100" :title="project.title" :content="project.content" :startDate="project.start_date" :endDate="project.end_date"/>
            </div>
        </div>
        <div class="d-flex justify-content-center mt-4">
            <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item"><a class="page-link" href="#" :disabled="curPage === 1" @click.prevent="prevPage()" >Previous</a></li>
                <li class="page-item" v-for="page in lastPage" :class="{'active' : curPage === page}"><a class="page-link" @click.prevent="changePage(page)">{{page}}</a></li>
                <li class="page-item"><a class="page-link" href="#" :disabled="curPage === lastPage" @click.prevent="nextPage()">Next</a></li>
            </ul>
        </nav>
        </div>

    </div>
</template>

<style scoped lang="scss">

</style>