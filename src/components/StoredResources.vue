<template>
  <ul class="resources-list">
    <learn-resource
      v-for="(resource, index) in resources"
      :key="index"
      :title="resource.title"
      :desc="resource.desc"
      :link="resource.link"
      :deleteresource="deleteresource"
      :index="index"
    ></learn-resource>
  </ul>
</template>
<script>
import LearnResource from "./LearnResource.vue";

export default {
  components: { LearnResource },
  name: "StoredResources",
  inject: ["StoredResources", "deleteresource"],
  props: {
    resources: {
      type: Array,
      default: () => [],
    },
  },
};
</script>
<style>
.resources-list {
  width: 700px;
  box-shadow: 0 2px 8px rgb(0 0 0 / 26%);
  border-radius: 20px;
  height: 500px;
  margin: 0 auto;
  padding: 20px 0;
}
.resource-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  text-align: left;
  padding: 0 10px;
  margin-bottom: 20px;
}
.resource-content {
  width: 80%;
}
.resource-title {
  text-transform: uppercase;
}
.resource-desc {
  text-align: justify;
  margin: 10px 0;
}
.resource-remove {
  width: 20%;
}
.resource-button {
  width: max-content;
  outline: none;
  border: none;
  padding: 15px 20px;
  color: white;
  background-color: #6a5af9;
  display: block;
  margin: auto auto 0;
  cursor: pointer;
  font-size: 18px;
  border-radius: 10px;
}
</style>
