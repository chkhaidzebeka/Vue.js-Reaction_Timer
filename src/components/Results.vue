<template>
  <div class="result">
    <p>Your reaction time is: {{ score }} ms.</p>
    <p>Your rank: {{ rank }}.</p>
  </div>
</template>

<script>
export default {
    props: {
        score: Number
    },
    data() {
        return {
            rank: null,
        }
    },
    mounted() {
        this.rank = 'Snail Pace...';
        if (this.score < 400) this.rank = 'Rapid Reflexes';
        if (this.score < 250) this.rank = 'Ninja Fingers';
        console.log(this.score)
    }
}
</script>

<style scoped>
    .result {
        background: #cfd0ff;
        border: 2px solid #190061;
    }
</style>