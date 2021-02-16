<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      click me
  </div>
</template>

<script>
export default {
    props: {
        delay: Number
    },
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    mounted() {
        console.log(this.delay)
        setTimeout(() => {
            this.showBlock = true;
            this.startTimer();
        },this.delay)
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10;
            },10)
        },
        stopTimer() {
            clearInterval(this.timer);
            this.showBlock = false;
            this.$emit('end', this.reactionTime)
        },
    }
}
</script>

<style>
    .block {
        width: 400px;
        border-radius: 5px;
        background:#0f303e;
        color: #fff;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>