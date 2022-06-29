<template>
  <container>
    <template v-slot:tabs>
      <div class="tabs-list">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          @click="this.currentTab = tab.component"
          class="tab-button"
        >
          {{ tab.title }}
        </button>
      </div>
    </template>
    <component :is="currentTab" :resources="this.initResource"></component>
  </container>
</template>
<script>
import Container from "./Container.vue";
import AddResource from "./AddResource.vue";
import StoredResources from "./StoredResources.vue";
export default {
  name: "Tabs",
  components: { Container, AddResource, StoredResources },
  provide() {
    return {
      addresource: this.addresource,
      deleteresource: this.deleteresource,
      StoredResources: this.StoredResources,
    };
  },
  data() {
    return {
      tabs: [
        {
          id: 1,
          component: StoredResources,
          title: "Stored Resources ",
        },
        {
          id: 2,
          component: AddResource,
          title: "Add Resources ",
        },
      ],
      currentTab: StoredResources,
      initResource: [],
    };
  },
  methods: {
    getLocalStorage(name) {
      return JSON.parse(localStorage.getItem(name));
    },
    addresource(title, desc, link) {
      let newData = {
        title: title,
        desc: desc,
        link: link,
      };
      this.initResource.push(newData);
      localStorage.setItem("storedData", JSON.stringify(this.initResource));
    },
    deleteresource(index) {
      console.log(index);
      this.initResource.splice(index, 1);
      localStorage.setItem("storedData", JSON.stringify(this.initResource));
    },
  },
  mounted() {
    console.log(this.addresource);
    const resources = this.getLocalStorage("storedData");
    if (resources && resources.length) {
      this.initResource = resources;
    }
  },
};
</script>
<style>
.tabs-list {
  margin: 30px 0;
}
.tab-button {
  width: max-content;
  outline: none;
  border: none;
  padding: 15px 20px;
  color: white;
  background-color: #6a5af9;
  cursor: pointer;
  font-size: 18px;
  border-radius: 10px;
  margin-right: 30px;
}
</style>
