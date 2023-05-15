<template>

<div>
    <button @click="startCountdown">Iniciar</button>
</div>    
<Timer :timer=timers[0] @countdown="countdown"></Timer>
<Timer :timer=timers[1] @countdown="countdown"></Timer>
</template>
 
<script>
import Timer from '@/components/Timer.vue'
export default {
    components: {
        Timer
    },
    data () {
        return {
            timers: [
                {name: 'Boss', initialSeconds: 10 },
                {name: 'Kish', initialSeconds: 15 },
            ]
        };
    },
    methods: {
        countdown(seconds) {
            console.log("olá "+seconds);
        }
    }
}
</script>