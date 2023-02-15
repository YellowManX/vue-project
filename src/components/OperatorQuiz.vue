<template>
  <div class="container">
    <div class="quiz" v-if="isQuizStarted">
      <div class="questions">
        {{ operandLeft }} {{ operator }} {{ operandRight }} ?
      </div>
      <div class="options">
        <button
          class="versions"
          @click="selectAnswer(answer)"
          v-for="(answer) in answers"
          :key="answer"
        >
          {{ answer }}
        </button>
      </div>
    </div>
    <div class="start" v-if="!isQuizStarted">
      <h5>Are you ready?</h5>
      <button class="back__btn" @click="startQuiz">Start</button>
    </div>
    <button class="back__btn" @click="$emit('onBack')">Back</button>
  </div>
</template>

<script>
export default {
  props: ["operator"],
  data() {
    return {
      isQuizStarted: false,
      operandLeft: null,
      operandRight: null,
      answers: [],
      expectedAnswer: null,
      errorCounter: 0,
      questionCounter: 0,
    };
  },
  methods: {
    startQuiz() {
      if (this.operator === "*") {
        this.operandLeft = parseInt(Math.random() * 16) + 2;
        this.operandRight = parseInt(Math.random() * 16) + 2;
      } else if (this.operator === "/") {
        this.operandRight = parseInt(Math.random() * 9) + 2;
        this.operandLeft =
          this.operandRight * (parseInt(Math.random() * 9) + 1);
      } else {
        this.operandRight = parseInt(Math.random() * 101) + 6;
        this.operandLeft =
          parseInt(Math.random() * 101) + this.operandRight * 2 + 1;
      }

      this.answers = [];
      this.isQuizStarted = true;

      const methods = {
        "+": (a, b) => a + b,
        "-": (a, b) => a - b,
        "*": (a, b) => a * b,
        "/": (a, b) => a / b,
      };

      const methodsToUse = methods[this.operator];

      const expectedAnswer = methodsToUse(this.operandLeft, this.operandRight);

      this.answers.push(Math.trunc(Math.abs(expectedAnswer + 1)));
      this.answers.push(Math.trunc(Math.abs(expectedAnswer - 2)));
      this.answers.push(Math.trunc(Math.abs(expectedAnswer + 2)));
      this.answers.push(Math.trunc(Math.abs(expectedAnswer - 1)));
      this.answers.push(Math.trunc(Math.abs(expectedAnswer - 3)));
      this.answers.push(Math.trunc(Math.abs(expectedAnswer + 3)));

      this.answers[parseInt(Math.random() * this.answers.length)] =
        expectedAnswer;

      this.expectedAnswer = expectedAnswer;
    },
    selectAnswer(answerSelected) {
      if (answerSelected !== this.expectedAnswer) {
        alert("WRONG ANSWER");
        this.errorCounter++;
      }
      this.startQuiz();
      this.questionCounter++;

    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
.quiz {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 30px;
}
.questions {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
  font-weight: 700;
  border: 2px solid #10aeb2;
  width: 130px;
  padding: 10px;
}
.options {
  display: flex;
  gap: 10px;
}
.start {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-bottom: 15px;
}
.versions {
  background-color: #10aeb2;
}
.back__btn {
  width: 100px;
}
.bg__btn {
  background-color: red;
}
</style>
