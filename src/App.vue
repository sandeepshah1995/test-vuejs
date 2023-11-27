<template>
  <div id="app">
    <UrlPreview />
  </div>
</template>

<script>
import UrlPreview from "@/components/UrlPreview.vue";

export default {
  components: {
    UrlPreview,
  },
};
</script>

<style>
/* Add global styles here */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
