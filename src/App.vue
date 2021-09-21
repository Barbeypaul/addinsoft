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

export default {
  name: "App",
  components: {
    Header,
    Tableau,
  },
};
</script>
