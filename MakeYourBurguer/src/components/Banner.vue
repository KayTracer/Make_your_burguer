<template>
  <div id="main-banner">
    <h1>Make Your Burguer</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>
<style scoped>
#main-banner {
  background-image: url("/img/burger.jpg");
  background-size: cover;
  background-position: 0 -250px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  height: 650px;
  margin-bottom: 50px;
}

#main-banner h1 {
  color: #fff;
  background-color: #222;
  font-size: 60px;
  padding: 20px 40px;
  text-align: center;
}
</style>
