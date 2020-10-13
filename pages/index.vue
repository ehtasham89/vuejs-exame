<template>
<div>
  <v-row>
    <v-col
        cols="6"
        sm="4"
      >
    <v-card
          class="pa-2"
          outlined
          tile
        >
          Your Name: {{name}}
        </v-card>
    </v-col>
    <v-col
        cols="6"
        sm="4"
      >
        <v-card
          class="pa-2"
          outlined
          tile
        >
          Current Question: {{currentQuestion.text}}
        </v-card>
      </v-col>
    <v-col
        cols="6"
        sm="4"
      >
        <v-card
          class="pa-2"
          outlined
          tile
        >
          Total Questions: {{getTotalQuestions()}}
        </v-card>
      </v-col>

      <v-col
        cols="6"
        sm="4"
      >
        <v-card
          class="pa-2"
          outlined
          tile
        >
          Total Score: {{getResult()}}
        </v-card>
      </v-col>
  </v-row>

  <v-row>
    <v-col>
      <question :question="currentQuestion" v-show="isVisible" />
    </v-col>
  </v-row>

  <v-row v-show="!isVisible">
    <v-col>
      <h3>Thank you! :)</h3>
    </v-col>
  </v-row>
</div>
</template>

<script>
import Question from '~/components/Question.vue'
import QuestionsList from '~/store/questions.js'
//console.log(QuestionsList);
export default {
 
  data() {
    return {
      name: "Ehtasham",
      index: 0,
      questionsList: QuestionsList,
      answerList: [{id: 0, score: 0}],
      currentQuestion: QuestionsList[0],
      isVisible: true
    }
  },
  components: {
    Question
  },
  mounted() {
    this.$nuxt.$on('collect-answer', answer => {
     this.collAnswer(answer);
    })
  },
  methods: {
    collAnswer(answer) {
      this.answerList.push(answer);

      if ((this.questionsList.length - 1) > this.index) { 
          this.index++;

          this.currentQuestion = this.questionsList[this.index];
      } else {
        this.isVisible = false;
      }
    },
    getResult() {
      return this.answerList.map(e => e.score).reduce((a, b) => a + b);
    },
    getTotalQuestions() {
      return this.questionsList.length
    }
  },
  
}
</script>
