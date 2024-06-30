<script>
export default {
    data() {
        return {
            
        }
    },

    props: {
        title: String,
        content: String,
        startDate: String,
        endDate: String,
    }
};
</script>

<template>
<div class="card" style="width: 18rem">
    <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">
            {{ content }}
        </p>
        <p> Data inizio: {{ startDate }}</p>
        <p> Data fine: {{ endDate }}</p>
    </div>
</div>
</template>

<style scoped lang="scss">
</style>