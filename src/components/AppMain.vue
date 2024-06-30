<script>
import axios from 'axios';

export default {
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
</template>

<style scoped lang="scss">

</style>