<template>
  <div class="wrapper">
    <header>
      <div><img alt="" class="logo" src="../assets/logo.png"/></div>
      <div>Shapkin</div>
      <div class="theme">
        <div>Темная тема</div>
        <RockerSwitch/>
      </div>
    </header>
    <main></main>
    <footer>
      <div>191-362</div>
      <div>Шапкин Давид Димитров</div>
      <div>09.07.2021</div>
    </footer>


  </div>
</template>

<script>
// Import package
import RockerSwitch from "vue-rocker-switch";
// Import styles
import "vue-rocker-switch/dist/vue-rocker-switch.css";


export default {
  name: "App",
  components: {
    RockerSwitch
  }
};
</script>

<style scoped>
header {
  background-color: antiquewhite;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: bisque;
}

.wrapper {
  margin-right: 10%;
  margin-left: 10%;
}

.logo {
  width: 40%;

}
</style>
