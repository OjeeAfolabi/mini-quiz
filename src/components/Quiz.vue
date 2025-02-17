<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { toRefs } from 'vue'
const props = defineProps({
  title: String,
  questions: Array,
  answers: Array,
  option: String,
})

const { title, questions, answers} = toRefs(props)

const onDrop = (event, questions) => {
  const answerId = event.dataTransfer.getData('answerId')
  const answer = answers.value.find((a) => a.id == answerId)
  if (answer && answer.text === questions.answer) {
    alert('Correct!')
  } else {
    alert('Wrong!')
  }
};

const onDragStart = (event, answer) => {
  event.dataTransfer.setData('answerId', answer.id)
};

const onTouchStart = (event, answer) => {
  event.dataTransfer = {
    setData: (type, id) => {
      event.dataTransfer[type] = id;
    },
    getData: (type) => {
      return event.dataTransfer[type];
    },
  };
  event.dataTransfer.setData('answerId', answer.id);
};

const onTouchEnd = (event, question) => {
  const answerId = event.dataTransfer.getData('answerId');
  const answer = answers.value.find(a => a.id == answerId);
  if (answer && answer.text === question.answer) {
    alert('Correct!');
  } else {
    alert('Wrong!');
  }
};

</script>

<template>
  <div id="body" class="md:m-8 sm:m-2 border-1 border-gray-300 md:p-4 sm:p-4">
    <div id="title" class="md:text-3xl sm:text-xl">{{ title }}</div>
    <div class="questions">
      <div
        class="question md:text-xl sm:text-base md:mt-1 sm:mt-0.5"
        @drop.prevent="(event) => onDrop(event, questions)"
        @dragover.prevent
        @touchend.prevent="(event) => onTouchEnd(event, questions)"
      >
        {{ questions.question }}
      </div>
    </div>
    <div id="anss" class="answers flex-col w-[20%] md:w-[20%] md:gap-6 sm:gap-3">
      <div
        id="ans"
        v-for="answer in answers"
        :key="answer.id"
        class="answer border-1 border-amber-500 md:p-2 sm:p-1 rounded md:mt-6 sm:mt-2.5 hover:bg-amber-200"
        draggable="true"
        @dragstart="(event) => onDragStart(event, answer)"
        @touchstart="(event) => onTouchStart(event, answer)"
      > {{ answer.option}}
        {{ answer.text}}
      </div>
    </div>
  </div>
</template>

<style scoped></style>
