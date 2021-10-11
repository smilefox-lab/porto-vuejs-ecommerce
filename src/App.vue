<template>
  <div id="app">
    <article>
      <header>
        <h1>
          How good are you at front-end development?
          <!-- {{ console.log("header") }} -->
        </h1>
      </header>
      <template v-if="!isEnd">
        <section>
          <p>
            Question {{ (currentQuestion = 1) }} out of {{ questions.length }}
          </p>
          <Question
            :question="questions[currentQuestion]"
            @nextQuestion="nextQuestion"
          />
        </section>
      </template>
      <template v-else>
        <Result :result="result" />
      </template>
    </article>
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Result from "./components/Result.vue";
// import './styles/style.scss'
export default {
  name: "App",

  components: {
    Question,
    Result,
  },
  data() {
    return {
      questions: [
        {
          title: "What is CSS?",
          answers: [
            { text: "Controlled Sporadic Spasms" },
            { text: "Critical Stylish Severity" },
            { text: "Cascading Style Sheets", isCorrect: true },
          ],
        },
        {
          title: "What is not a front-end  tool?",
          answers: [
            { text: "Webpack" },
            { text: "Tortilla", isCorrect: true },
            { text: "Gulp" },
          ],
        },
        {
          title: "What is an HTML tag for an ordered list?",
          answers: [
            { text: "<ol>", isCorrect: true },
            { text: "<list>" },
            { text: "<ul>" },
          ],
        },
      ],
      currentQuestion: 0,
      correctAnswers: 0,
    };
  },
  computed: {
    isEnd() {
      return this.questions.length <= this.currentQuestion;
    },

    result() {
      return Math.round((this.correctAnswers / this.questions.length) * 100);
    },
  },

  // nextQuestion() will increment the counter of correct answers (correctAnswers) if the answer submitted by the user is correct
  methods: {
    nextQuestion(answer) {
      if (answer.isCorrect) {
        this.correctAnswers++;
      }

      this.currentQuestion++;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
