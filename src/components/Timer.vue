<template>
    <h1>{{ timerText }}</h1>
</template>

<script>
export default {
    emits: ['countdown'],
    props: {
        timer: Object,
        currentTimer: Object
    },
    computed: {
        timerText() {
            return this.timer.name + ': ' + this.remainingSeconds;
        }
    },
    data () {
        return {
            remainingSeconds: 10,
        };
    },
    watch: {
        remainingSeconds: {
            handler: function(oldVal, newVal) {
                this.decreaseTimer();
            },            
        },
        currentTimer: {
            handler: function(oldVal, newVal) {
                this.decreaseTimer();
            },            
        }
    },
    mounted() {
        this.startCountdown();
    },
    methods: {
        decreaseTimer() {
            console.log("remSeconds", this.remainingSeconds);
            if (this.remainingSeconds > 0) {
                setTimeout(() => {        
                    if (this.currentTimer.name == this.timer.name) {
                        this.remainingSeconds--;
                    }
                }, 1000);
            }
            else {
                this.onCountdownEnd();
            }
        },
        startCountdown() {
            this.remainingSeconds = this.timer.initialSeconds;
        },
        onCountdownEnd() {
            this.remainingSeconds = this.timer.initialSeconds;
            this.$emit('countdown', this.timer);
        },
    }
}
</script>