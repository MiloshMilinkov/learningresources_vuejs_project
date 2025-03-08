<template>
    <TheHeader title="Remember what to Learn."></TheHeader>
 <StoredResources :resources="storedResources"></StoredResources>
</template>

<script>
import StoredResources from './components/learning-resources/StoredResources.vue';
import TheHeader from './components/layouts/TheHeader.vue';
    export default {
        components:{
            StoredResources,
            TheHeader
        },
        data() {
            return {
                storedResources:[
                    {
                        id: 'officical-guide', 
                        title:'Official Guide', 
                        description: 'This is an official guide for VueJS.',
                        link: 'https://vuejs.org/guide/introduction'
                    },
                    {
                        id: 'google', 
                        title:'Google', 
                        description: 'learn to google.',
                        link: 'https://google.com'
                    },
                ]
            }
        },
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

    * {
    box-sizing: border-box;
    }

    html {
    font-family: 'Roboto', sans-serif;
    }

    body {
    margin: 0;
    }
</style>