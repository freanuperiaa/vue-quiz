<template>
    <div>
        <b-nav tabs>
            <b-nav-item disabled><b>Vue Quiz App</b></b-nav-item>
            <b-nav-item disabled>Counter: {{ numTotal + 1 }}/10</b-nav-item>
            <b-nav-item>Correct Answers: {{ numCorrect }}</b-nav-item>
        </b-nav>
    </div>
</template>

<script>
export default {
    props: {
        numCorrect: Number,
        numTotal: Number,
    },
}
</script>

<style scoped>
</style>