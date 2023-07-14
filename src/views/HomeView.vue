<template>
  <div class="full-height">
    <HomePageComponent/>
  </div>
</template>

<script>
// @ is an alias to /src

import HomePageComponent from "../PageComponents/HomePageComponent.vue"
export default {
  name: "HomeView",
  components: {
    HomePageComponent
  },
};
</script>
<style>
</style>
