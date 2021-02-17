<template>
  <div class="result">
    <p>Your reaction time is: {{ reactionTime }} ms.</p>
    <p>Your rank: {{ rank }}.</p>
    <p>Your score: {{ elements }} x {{ reactionTime }} = {{ calculatedScore }}</p>
    <p>The best reactionTime so far: {{ theBestScore }}</p>
  </div>
</template>

<script>
export default {
    props: {
        reactionTime: Number,
        elements: Number
    },
    data() {
        return {
            rank: null,
            calculatedScore: this.elements * this.reactionTime
        }
    },
    computed: {
        theBestScore() {
            return localStorage.getItem("the_best_score") || 0
        },

    },
    mounted() {
        this.rank = 'Snail Pace...';
        if (this.reactionTime < 400) this.rank = 'Rapid Reflexes';
        if (this.reactionTime < 250) this.rank = 'Ninja Fingers';
    }
}
</script>

<style scoped>
    .result {
        padding: 10px;
        background: #cfd0ff;
        border: 2px solid #190061;
    }
    p {
        margin: 10px auto;
    }
    p:last-child {
        border-top: 2px solid #0d1236;
        padding-top: 5px;
    }
</style>