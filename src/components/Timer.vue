<template>
    <h1>{{ timerText }}</h1>
    <h2>{{ remainingSeconds }}</h2 >
</template>

<script>
export default {
    emits: ['countdown'],
    props: {
        timer: Object   
    },
    computed: {
        timerText() {
            return this.timer.name + ': ' + this.c;
        }
    },
    data () {
        return {
            remainingSeconds: 0,
            counting: false,
            header: 'Timer:'
        };
    },
    watch: {
        remainingSeconds: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.remainingSeconds--;
                    }, 1000);
                }
            },
            immediate: true // This ensures the watcher is triggered upon creation
        }
    },
    mounted() {
        this.remainingSeconds = this.timer.initialSeconds;
    },
    methods: {
        startCountdown() {
            this.counting = true;
            this.remainingSeconds = this.timer.initialSeconds;
        },
        onCountdownEnd() {
            this.counting = false;
            this.$emit('countdown', this.timer.name);
        },
    }
}
</script>