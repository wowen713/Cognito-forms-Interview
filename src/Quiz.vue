<template>
  <div id="QuizPage">
    <div class="startbuttonclass">
      <button class="startbutton" v-on:click="State = 2" :hidden="State != 1">
        <h1 style="font-family: ubuntu">start quiz</h1>
      </button>
    </div>
    <div class="questions" :hidden="State != 2">
      <h3>Question {{ IndexNum + 1 }}:</h3>
      <p>{{ questions[IndexNum].text }}</p>
    </div>
    <div id="answers" :hidden="State != 2">
      <div v-for="answer in questions[IndexNum].answers" :key="answer">
        <input
          type="radio"
          :id="answer"
          :value="answer"
          v-model="selected[IndexNum]"
          v-on:click="Answered = true"
        />
        <label :for="answer">{{ answer }}</label>
        <p />
      </div>
    </div>
    <button
      class="NextButton"
      v-on:click="increment"
      :disabled="selected[IndexNum] == null"
      :hidden="State != 2"
    >
      Next
    </button>
    <div id="lastpage">
      <div :hidden="State != 3">
        <div v-for="index in questions.length" :key="index">
          <p>Question {{ index }}: {{ questions[index - 1].text }}</p>
          Your Answer: <strong>{{ selected[index - 1] }}</strong>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import question from "./questions";

export default {
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      State: 1,
      IndexNum: 0,
      selected: [],
    };
  },
  methods: {
    increment() {
      if (this.IndexNum < question.length - 1) {
        this.IndexNum++;
      } else {
        this.State = 3;
      }
    },
  },
};
</script>


<style scoped>
.startbuttonclass {
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
.startbutton {
  background-color: white;
  color: black;
  border: 2px solid blue;
  border-radius: 6px;
  text-align: center;
  transition-duration: 0.5s;
}
.startbutton:hover {
  background-color: blue;
  color: white;
  border: 2px solid blue;
  border-radius: 6px;
  text-align: center;
}

.questions {
  text-align: left;
}

.NextButton {
  background-color: white;
  border-radius: 6px;
  border: 2px solid blue;
  text-align: center;
  transition-duration: 0.5s;
}
.NextButton:disabled {
  background-color: white;
  border-radius: 6px;
  border: 2px solid lightblue;
  text-align: center;
  pointer-events: none;
}
.NextButton:hover {
  background-color: blue;
  color: white;
  border: 2px solid blue;
  border-radius: 6px;
  text-align: center;
}
</style>