<template>
  <base-card class="card-container">
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      class="custom-button"
      >Objetivos</base-button
    >
    <!-- Adicionei -->
    <base-button
      @click="setSelectedTab('archived-resource')"
      :mode="archiveResButtomMode"
      class="custom-button"
      >Objetivos feitos</base-button
    >
    <!-- Adicionei -->
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      class="custom-button"
      >Adicionar objetivo</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
import ArchivedResource from './ArchivedResource.vue';

export default {
  components: { StoredResources, AddResource, ArchivedResource },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'lavar-roupa',
          title: 'Lavar roupa',
          description: 'Separar brancas das coloridas',
          link: '',
        },
        {
          id: 'aprender-vue',
          title: 'Aprender Vue.js',
          description: 'Aprender o conceito de forms do Vue.js',
          link: 'https://vuejs.org',
        },
      ],
      archivedResources: [],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
      archivedResources: this.archivedResources,
      archiveResource: this.archiveResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
    archiveResButtomMode() {
      return this.selectedTab === 'archived-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },

    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource); //push, but at the beggining of the array
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
    archiveResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      const deletedResource = this.storedResources.splice(resIndex, 1)[0];
      this.archivedResources.push(deletedResource);
    },
  },
};
</script>

<style scoped>
.card-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.custom-button {
  flex-grow: 1;
  margin: 0 5px;
  width: 100%;
}
</style>
