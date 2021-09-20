<template>
  <div>
    <header>
      <Header></Header>
    </header>
    <div>
      <Tableau msg="Welcome to Your Vue.js App" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tableau from "./components/Tableau.vue";
// import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Tableau,
  },
  data() {
    return {
      info: null,
    };
  },
};
</script>
