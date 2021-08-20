<template>
  <div class="result">
    <div class="title" :class="{ titleSuccessfuly: resultIndex === 1 }">
      {{ results[resultIndex].title }}
    </div>
    <div class="desc">
      {{ results[resultIndex].desc }}
      <div class="results" v-if="questionsAnswered === questions.length">
        <h3>Results</h3>
        <div>Total Correct : {{ totalCorrect }}</div>
        <div>Questions Answered : {{ questionsAnswered }}</div>
        <div>Questions Length : {{ questions.length }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    "results",
    "totalCorrect",
    "questionsAnswered",
    "questions",
    "soundActive",
  ],
  data() {
    return {
      index: 0,
    };
  },
  computed: {
    resultIndex() {
      // let index = 0;

      this.results.forEach((e, i) => {
        if (e.min <= this.totalCorrect && e.max >= this.totalCorrect) {
          this.index = i;
        }
      });

      return this.index;
    },
  },

  mounted() {
    if (this.soundActive) {
      if (this.index === 0) {
        let audio = new Audio("https://freesound.org/data/previews/162/162473_311243-lq.mp3");
        audio.play();
      } else {
        let audio = new Audio("https://freesound.org/data/previews/401/401121_7725148-lq.mp3");
        audio.play();
      }
    }
  },
};
</script>

<style scoped></style>
