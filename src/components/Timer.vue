<template>
    <h1>{{ header + number }}</h1>

<li v-for="item in items" :key="item.id">{{item.label}}</li>
</template>

<script>
export default {
    props: ['number'],
    data () {
        return {
            header: 'Shopping List App',
            items: [
                {id: 1, label:'10 party hats'},
                {id: 2, label:'2 board games'},
                {id: 3, label:'20 cups'}]
        }
    },  
    methods: {
    },
    created () {
    }
}
</script>