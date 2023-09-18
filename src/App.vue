<template>
  <div class="app">
    <div class="fight" id="fight">
      <div class="info">
            <h1>Witaj Amazonko.</h1>
            <p>Tutaj możesz wkleić swoje walki i wsady. Oszczędzi Ci to czas.</p>
        </div>
      <div class="component-container">
        <div class="component">
          <HelloWorld msg="Welcome to Your Vue.js App" />
        </div>
        <div class="component">
          <AmazonCatch /> <!-- Dodaj komponent AmazonCatch -->
        </div>
      </div>
    </div>
    <footer @click="scrollToFight">
      <p>Do góry</p>
    </footer>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import AmazonCatch from './components/AmazonCatch.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    AmazonCatch // Dodaj komponent AmazonCatch
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
.info {
    width: 90%;
    text-align: center;
    margin: 0 auto;

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

.component-container {
  display: flex;
  justify-content: space-between; /* Rozłożenie komponentów poziomo */
}

.component {
  width: 48%; /* Szerokość każdego komponentu, aby zajmowały po połowie */
}

@media (max-width: 767px) {
  .app {
    padding: 10px;
    max-width: 90%;
  }
}
</style>
