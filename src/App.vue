<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <QuestionList></QuestionList>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import QuestionList from './components/QuestionList.vue';
import QuestionItem from './components/QuestionItem.vue';

export default {
  name: 'app',
  components: {
    QuestionItem,
    QuestionList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
