<script>
import axios from 'axios';

import ProjectCard from './ProjectCard.vue';

export default {

    components: {
        ProjectCard
    },

    data() {
        return {
            projects: []
        }
    },

    created(){
        axios.get('http://127.0.0.1:8000/api/projects').then((resp) => {

            // console.log(resp);

            // Prelevo i dati e li assegno a projects
            this.projects = resp.data.result;
        })
    }
}
</script>

<template>
    <h1>App Main</h1>
    <div class="container">
        <div class="row">
            <div class="col" v-for="project in this.projects">
                <ProjectCard :title="project.title" :content="project.content" :startDate="project.start_date" :endDate="project.end_date"/>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">

</style>