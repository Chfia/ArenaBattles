<template>
  <div>
    <h1>Vue.js Log Filter</h1>

    <!-- Pole tekstowe do wklejania logów -->
    <textarea v-model="logsText" placeholder="Wklej logi tutaj"></textarea>

    <!-- Przycisk do uruchomienia filtrowania -->
    <button @click="filterLogs">Filtruj</button>

    <!-- Wyświetlanie przefiltrowanych logów -->
    <div>
      <h2>Przefiltrowane Logi:</h2>
      <ul>
        <li v-for="(log, index) in filteredLogs" :key="index" v-html="log"></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      logsText: '', // Dane wklejone przez użytkownika
      filteredLogs: [] // Przechowuje przefiltrowane logi
    };
  },
  methods: {
    filterLogs() {
      // Rozdziel logi na linie
      const lines = this.logsText.split('\n');
      const filteredLogs = [];

      let currentLog = ''; // Przechowuje bieżący log

      // Lista zwierząt do odfiltrowania
      const zwierzetaDoFiltrowania = ['Wilk', 'Jeleń', 'Lis', 'Przepiórka', 'Dzik', 'PRZEGRAŁEŚ', 'Słoń', 'Szejk Am-Al', 'przestępca', 'zwierzę' ];

      // Przeglądaj każdą linię
      for (const line of lines) {
        if (line.match(/^\d+\.\s\d+/)) {
          // Jeśli linia rozpoczyna nowy log, dodaj poprzedni log do wyników
          if (currentLog.trim() !== '' && !zwierzetaDoFiltrowania.some(zwierze => currentLog.includes(zwierze))) {
            filteredLogs.push(currentLog.trim());
          }
          currentLog = line;
        } else {
          // W przeciwnym razie dodaj linię do bieżącego logu
          currentLog += '<br>' + line;
        }
      }

      // Dodaj ostatni log, jeśli nie zawiera zwierzęcia
      if (currentLog.trim() !== '' && !zwierzetaDoFiltrowania.some(zwierze => currentLog.includes(zwierze))) {
        filteredLogs.push(currentLog.trim());
      }

      this.filteredLogs = filteredLogs;
    }
  }
};
</script>

<style scoped>
/* Możesz dodać stylizację CSS tutaj */
</style>
