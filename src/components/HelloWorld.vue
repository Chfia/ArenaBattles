<template>
  <div>
    <div class="info">
      <h1>Witaj Amazonko.</h1>
      <p>Tutaj możesz wkleić swoje walki z dziennika z zakładki walka. Zostaną one przefiltrowane tak aby
        usunąć walki ze zwierzętami i będziesz miała gotowy wpis do wklejenia na forum. Oszczędzi Ci to czas.</p>
    </div>

 
      <textarea class="fight" v-model="logsText" placeholder="Wklej logi tutaj"></textarea>

    <button @click="filterLogs">Filtruj</button>
    <button v-if="filteredLogs.length > 0" @click="copyResults">Kopiuj Wyniki</button>


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
      logsText: '',
      filteredLogs: []
    };
  },
  methods: {
    filterLogs() {
      const lines = this.logsText.split('\n');
      const filteredLogs = [];

      let currentLog = ''; 

      const zwierzetaDoFiltrowania = ['Wilk', 'Jeleń', 'Lis', 'Przepiórka', 'Dzik', 'PRZEGRAŁEŚ', 'Słoń', 'Szejk Am-Al', 'przestępca', 'zwierzę'];

      for (const line of lines) {
        if (line.match(/^\d+\.\s\d+/)) {
          if (currentLog.trim() !== '' && !zwierzetaDoFiltrowania.some(zwierze => currentLog.includes(zwierze))) {
            filteredLogs.push(currentLog.trim());
          }
          currentLog = line;
        } else {
          currentLog += '<br>' + line;
        }
      }

      if (currentLog.trim() !== '' && !zwierzetaDoFiltrowania.some(zwierze => currentLog.includes(zwierze))) {
        filteredLogs.push(currentLog.trim());
      }

      this.filteredLogs = filteredLogs;
    },
    copyResults() {
      const tempDiv = document.createElement('div');
      tempDiv.innerHTML = this.filteredLogs.join('<br>');

      document.body.appendChild(tempDiv);

      const range = document.createRange();
      range.selectNodeContents(tempDiv);
      window.getSelection().removeAllRanges();
      window.getSelection().addRange(range);

      try {
        document.execCommand('copy');
      } catch (err) {
        console.error('Nie udało się skopiować jako HTML: ', err);
      }

      document.body.removeChild(tempDiv);

      window.getSelection().removeAllRanges();
    }
  }
};
</script>


<style scoped>
.info {
  width: 90%;
  text-align: center;
  margin: 0 auto;

}
.fight {
  width: 90%;
  max-width: 600px;
  height: 200px;
  padding: 10px;
  margin-top: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  resize: none;
}
</style>
