<template>
  <div id="app">
    <TodoHeader></TodoHeader>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

// var my_cmp = {
//   template: '<div>hi?</div>'
// };

// new Vue({
//   el: '#app',
//   components: {
//     'my-cmp': my_cmp
//   }
// })
export default {
  components: {
    'TodoHeader': TodoHeader
  }
}
</script>

<style>

</style>
