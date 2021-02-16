<template>
  <div class="main" v-if="showBlock">
    <p>Click {{ index }}th element</p>
    <div class="container">
        <div class="block" @click="validate(index)" v-for="(index,el) in elements" :key="index"></div>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        delay: Number,
        index: Number,
        elements: Number,
    },
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0,
        }
    },
    mounted() {
        setTimeout(() => {
            this.showBlock = true;
            this.$emit('started');
            this.startTimer();
        },this.delay*1000)
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10;
            },10)
        },
        validate(userIndex) {
            clearInterval(this.timer);
            this.showBlock = false;

            if (userIndex != this.index) {
                this.$emit('end', this.reactionTime,false);
                alert("you failed");
                return false;
             } else this.$emit('end', this.reactionTime,true);
        }
    }
}
</script>

<style>
    .main {
        max-width: 90%;
        border-radius: 5px;
        background:#0f303e;
        color: #fff;
        text-align: center;
        padding: 60px 0;
        margin: 40px auto;
    }
    .container {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        width: 70%;
        margin: 10px auto;
        position: relative;
    }

    .block {
        cursor: pointer;
        background: #6db46d;
        height: 100px;
        width: 100px;
        margin: 10px;
    }

    .block:hover {
        transform: scale(1.1);
        transition-duration: 2ms;
    }
</style>