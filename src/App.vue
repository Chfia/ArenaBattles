<template>
  <div class="app">
    <div class="fight" id="fight">
      <HelloWorld msg="Welcome to Your Vue.js App" />
    </div>
    <footer @click="scrollToFight">
      <p>Do góry</p>
    </footer>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    scrollToFight() {
      const fightSection = document.getElementById("fight");
      if (fightSection) {
        fightSection.scrollIntoView({ behavior: "smooth" });
      }
    },
  },
};
</script>

<style scoped>
.app {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #274d2a;
  scroll-behavior: smooth;
}

footer {
  position: fixed;
  bottom: 0;
  right: 0;
  background-color: #333;
  color: #fff;
  padding: 10px;
  text-align: center;
  cursor: pointer;
}

@media (max-width: 767px) {
  .app {
    padding: 10px;
    max-width: 90%;
  }
}
</style>
