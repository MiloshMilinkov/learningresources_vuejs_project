<template>
    <BaseCard>
        <BaseButton @click="setSelectedTab('StoredResources')" :mode="storedResourceButtonMode">Stored Resources</BaseButton>
        <BaseButton @click="setSelectedTab('AddResource', null)" :mode="addResourceButtonMode">Add Resources</BaseButton>
    </BaseCard>
    <KeepAlive><component :is="selectedTab" :editingResource="editingResource"></component></KeepAlive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: { StoredResources, AddResource },
    data() {
        return {
            selectedTab: 'StoredResources',
            storedResources: [
                {
                    id: 'officical-guide',
                    title: 'Official Guide',
                    description: 'This is an official guide for VueJS.',
                    link: 'https://vuejs.org/guide/introduction'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to Google.',
                    link: 'https://google.com'
                }
            ],
            editingResource: null
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource,
            editResource: this.startEditingResource
        };
    },
    methods: {
        setSelectedTab(tab, resource = null) {
            this.selectedTab = tab;
            this.editingResource = resource;
        },
        addResource(title, description, url, id = null) {
            if (id) {
                // If ID exists, update the resource
                const index = this.storedResources.findIndex(res => res.id === id);
                if (index !== -1) {
                    this.storedResources[index] = { id, title, description, link: url };
                }
            } else {
                // Otherwise, add a new resource
                const newResource = { id: new Date().toISOString(), title, description, link: url };
                this.storedResources.unshift(newResource);
            }
            this.setSelectedTab('StoredResources');
        },
        removeResource(resId){
            const resIndex = this.storedResources.findIndex(res => res.id == resId);
            this.storedResources.splice(resIndex, 1);
        },
        startEditingResource(resId) {
            const resource = this.storedResources.find(res => res.id === resId);
            if (resource) {
                this.setSelectedTab('AddResource', resource);
            }
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