<template>
  <div>
    <h2 class="result-title">Your result:</h2>
    <p id="summary">
      You've given <span>{{ result }}%</span> of correct answers. {{ tip }}
    </p>
  </div>
</template>
          
<script>
export default {
  name: "Result",

  props: {
    result: Number,
  },

  computed: {
    tip() {
      if (this.result <= 30) {
        return "Don't give up and learn JavaScript!";
      } else if (this.result <= 50) {
        return "You can start your Junior Front-End Developer career at Dominos' Pizza!";
      } else if (this.result <= 90) {
        return "Well done! You're better than average!";
      }

      return "Send your CV to Google right now!";
    },
  },
};
</script>

<style scoped></style>
      