<template>
    <BaseCard>
        <BaseButton @click="setSelectedTab('StoredResources')" :mode="storedResourceButtonMode">Stored Resources</BaseButton>
        <BaseButton @click="setSelectedTab('AddResource')" :mode="addResourceButtonMode">Add Resources</BaseButton>
    </BaseCard>
    <KeepAlive><component :is="selectedTab"></component></KeepAlive>
</template>
<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
    components:{
            StoredResources,
            AddResource
    },
    data(){
        return{
            selectedTab:'StoredResources',
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
        };
    },
    provide(){
        return { resources: this.storedResources, addResource: this.addResource}
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addResource(title, description, url){
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            }
            this.storedResources.unshift(newResource);
            this.selectedTab = 'StoredResources'
        }
    },
    computed:{
        storedResourceButtonMode(){
            return this.selectedTab === 'StoredResources' ? null : 'flat';
        },
        addResourceButtonMode(){
            return this.selectedTab === 'AddResource' ? null : 'flat';
        },
    }
}
</script>