<template>
  <div class="question">
    <h2>{{ question.title }}</h2>
    <ol class="options">
      <li
        v-for="(answer, index) in question.answers"
        :key="index"
        :class="
          choosenAnswer ? (answer.isCorrect || false ? 'green' : 'red') : ''
        "
      >
        <a href="#" @click="getAnswer(answer)">{{ answer.text }}</a>
      </li>
    </ol>
    <div v-if="choosenAnswer">
      <p class="answer" :class="{ correct: choosenAnswer.isCorrect || false }">
        <template v-if="choosenAnswer.isCorrect">Correct,</template>
        <template v-else>Incorrect, the correct answer is</template>
        {{ correctAnswer.text }}
      </p>
      <button @click="nextQuestion" class="btn">Next</button>
    </div>
  </div>
</template>
         
<script>
export default {
  name: "Question",

  props: {
    question: Object,
  },

  data() {
    return {
      choosenAnswer: null,
    };
  },

  watch: {
    question() {
      this.choosenAnswer = null;
    },
  },

  computed: {
    correctAnswer() {
      return this.question.answers.find((answer) => answer.isCorrect);
    },
  },

  methods: {
    getAnswer(answer) {
      if (this.choosenAnswer) {
        return;
      }

      this.choosenAnswer = answer;
    },

    nextQuestion() {
      this.$emit("nextQuestion", this.choosenAnswer);
    },
  },
};
</script>

<style scoped>
.green a::before {
  background: green;
}
.red a::before {
  background: red;
}
.correct {
  color: green;
}
</style>
       