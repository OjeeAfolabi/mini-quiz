<script setup>
import NavBar from './components/NavBar.vue'
import Quiz from './components/Quiz.vue'
import Footer from './components/Footer.vue'

const quizzes = [
  {
    id: 1,
    title: 'Question 1',
    questions: { id: 1, question: 'What is the capital of France?', answer: 'Paris' },
    answers: [
      { id: 1, text: 'Paris', option: "A." },
      { id: 2, text: 'Lagos', option: "B." },
      { id: 3, text: 'Madrid', option: "C." },
    ],
  },
 {
    id: 2,
    title: 'Question 2',
    questions: { id: 2, question: 'The square root of 7 is?', answer: '49' },
    answers: [
      { id: 1,  text: '14', option:"A."  },
      { id: 2,  text: '49', option:"B."  },
      { id: 3,  text: '144', option:"C."  },
    ],
  },
  {
    id: 3,
    title: 'Question 3',
    questions: {
      id: 2,
      question: 'Which of these is the largest organ in the body?',
      answer: 'Skin',
    },
    answers: [
      { id: 1, text: 'Heart' , option:"A." },
      { id: 2, text: 'Liver' , option:"B." },
      { id: 3, text: 'Skin'  , option:"C." },
    ],
  },
]
</script>

<template>
  <main>
    <NavBar />
    <div v-for="quiz in quizzes" :key="quiz.id">
      <Quiz :title="quiz.title" :questions="quiz.questions" :answers="quiz.answers" :option="quiz.option" />
    </div>
    <Footer />
  </main>
</template>

<style></style>
