<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container {
  background-color: #cce5ff;
  color: #004085;
  border: 2px solid #b8daff;
  border-radius: 5px;
  margin: 30px auto;
  padding: 10px;
  max-width: 400px;
}
</style>
