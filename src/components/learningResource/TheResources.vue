<template>
    <base-card>
       <base-button 
       @click="setSelectedTab('stored-resources')"
       :mode="storedResButtonMode">StoredResources</base-button>
       <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
       <component :is="selectedTab"></component>

</template>

<script>
 import StoredResources from './StoredResources.vue';
 import AddResource from './AddResources.vue';

  export default {
    components: {
        StoredResources,
        AddResource
    },

    data() {
         return {
            selectedTab: 'stored-resources',
            storedResources: [
                { 
                    id: "official-giude", 
                    title: 'The Official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                }
            ]
         }
    },

    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource
        };
    },

    computed: {
      storedResButtonMode() {
        return this.selectedTab === 'stored-resources' ? null : 'flat'
      },

      addResButtonMode() {
        return this.selectedTab === 'add resource' ? null : 'flat';
      }
    },

    methods:{
        setSelectedTab(tab) {
          this.selectedTab = tab;
        },
 
        addResource(title, description, url) {
          const newResource = {
            id: new Date().toISOString(),
            title: title,
            description: description,
            link: url
          };
          this.storedResources.unshift(newResource);
          this.selectedTab = 'stored-resources';
        },

        removeResource(resId) {
          const resIndex = this.storedResources.findIndex((res) => res.id === resId);
          this.storedResources.splice(resIndex, 1);   
        }
    }
  }


</script>


