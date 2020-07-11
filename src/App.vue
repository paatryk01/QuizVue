<template>
  <div id='app'>
    <Header 
      :numTotal="numTotal"
      :numCorrect="numCorrect"
    />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length" 
            :currentQuestion="questions[index]"
            :nextQ="nextQ"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
    
  </div>
</template>

<script>

import Header from './components/Header';
import QuestionBox from './components/QuestionBox'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    nextQ() {
      this.index++;
    },
    increment(isCorrect){
      if(isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted() {
    fetch('https://opentdb.com/api.php?amount=10&category=21&difficulty=medium&type=multiple', {
      method: 'get'
    })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      })
  }
}
</script>

<style>

#app {
  text-align: center;
  margin-top: 60px;

}

</style>
