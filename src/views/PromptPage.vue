<template>
  <div>
    <StatusBar/>
    <router-view></router-view>
  </div>
</template>

<script>
import StatusBar from "../components/StatusBar";
export default {
  name: "PromptPage",
  components: {
    StatusBar
  }
};
</script>


<style scoped>
</style>


