<template>

<div>
    <button @click="toggleCountdown">{{ buttonLabel }}</button>
</div>    
<div v-if="counting">
    <Timer :timer=timers[0] :currentTimer=currentTimer @countdown="countdown"></Timer>
    <Timer :timer=timers[1] :currentTimer=currentTimer @countdown="countdown"></Timer>
    <Timer :timer=timers[2] :currentTimer=currentTimer @countdown="countdown"></Timer>
    <Timer :timer=timers[3] :currentTimer=currentTimer @countdown="countdown"></Timer>
    <Timer :timer=timers[4] :currentTimer=currentTimer @countdown="countdown"></Timer>
</div>
</template>
 
<script>
import Timer from '@/components/Timer.vue'
import puftupFile from '@/assets/puftup_explode.mp3'
import animalTokensFile from '@/assets/animal_tokens.mp3'
import pauseDkc2File from '@/assets/pause_dkc2.mp3'

export default {
    components: {
        Timer
    },
    computed: {
        buttonLabel() {
            if (this.counting) return "Stop";
            return "Start";
        }
    },
    data () {
        let puftupAudio = new Audio(puftupFile);
        let animalTokensAudio = new Audio(animalTokensFile);
        let pauseDkc2Audio = new Audio(pauseDkc2File);
        return {
            counting: false,
            timers: [
                {name: 'Boss1', initialSeconds: 30, sound: puftupAudio},
                {name: 'Kish1', initialSeconds: 30, sound: pauseDkc2Audio},
                {name: 'Boss2', initialSeconds: 25, sound: puftupAudio},
                {name: 'Loot', initialSeconds: 5, sound: animalTokensAudio},
                {name: 'Kish2', initialSeconds: 30, sound: pauseDkc2Audio},
            ],
            currentTimer: undefined
        };
    },
    created() {
        this.currentTimer = this.timers[0]
    },
    methods: {
        countdown(timer) {
            timer.sound.play();
            this.getNextTimer();
        },
        getNextTimer() {
            let currentIndex = this.timers.indexOf(this.currentTimer);
            console.log('currentIndex', currentIndex);
            if (currentIndex == (this.timers.length-1)) {
                this.currentTimer = this.timers[0]; // Get first element
            } else {
                this.currentTimer = this.timers[currentIndex+1]; // Get Next element
            }
        },
        toggleCountdown() {
            this.currentTimer = this.timers[0];
            this.counting = !this.counting;
        }
    }
}
</script>