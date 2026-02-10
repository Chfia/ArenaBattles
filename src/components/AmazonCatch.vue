<template>
    <div>
      <textarea class="amCatch" v-model="logsText" placeholder="Wklej wsady tutaj"></textarea>
      <button @click="filterLogs">Filtruj</button>
      <button v-if="filteredLogs.length > 0" @click="copyResults">Kopiuj Wyniki!</button>
  
      <div>
        <h2>Przefiltrowane wsady:</h2>
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
        const wsadyDoFiltrowania = ['porwała'];
  
        this.filteredLogs = lines
          .filter((line) => {
            return wsadyDoFiltrowania.some((wsad) => line.includes(wsad));
          })
          .map((line) => {
            return line.replace(/^\d+\.\s\d+\s*/, '');
          });
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
  .amCatch {
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
  