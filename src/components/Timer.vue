<template>
    <h1>{{ timerText }}</h1>
</template>

<script>
export default {
    emits: ['countdown'],
    props: {
        timer: Object,
        c: Object
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
            handler(value) {
                console.log("value", value)
                if (value > 0) {
                    setTimeout(() => {
                        this.remainingSeconds--;
                    }, 1000);
                }
                else {
                    this.onCountdownEnd();
                }
            },            
        }
    },
    mounted() {
        this.startCountdown();
    },
    methods: {
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