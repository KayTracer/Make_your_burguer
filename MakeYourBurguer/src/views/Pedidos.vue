<template>
  <div class="main-container">
    <h1>Gerenciar pedidos:</h1>
    <Dashboards />
  </div>
</template>

<script>
import Dashboards from "../components/Dashboards.vue";

export default {
  name: "Pedidos",
  components: { Dashboards },
};
</script>
<style scoped>
.main-container {
  flex: 1;
}
</style>
