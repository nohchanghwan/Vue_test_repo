<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems" ></TodoFooter>    
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  
  data: function() {
    return {
      todoItems:  []
    }
  },
  methods: {
    addOneItem: function(todoItem) {
      var obj = {completed: false, item: todoItem};
      //저장하는 로직, JSON.stringify는 자바스크립트 객체를 스트링으로 변환시켜준다.
      localStorage.setItem(todoItem, JSON.stringify(obj));
      //push란 자바스크립트 api로 배열요소를 추가
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index) {
      //오브젝트가 아닌 특정 문자열 키값을 지우는 로직
      localStorage.removeItem(todoItem.item);
      // splice() api는 해당 아이템을 삭제하게 된다.
      this.todoItems.splice(index, 1);
    },
    toggleOneItem: function(todoItem, index) {
      this.todo.Items[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems: function() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created: function() {
      // 로컬스토리지에 있는 데이터를 갖고오는 로직 
    if (localStorage.length > 0) {
      for(var i = 0; i < localStorage.length ; i ++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
            this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            // this.todoItems.push(localStorage.key(i));    
        }
      }
    }   
  },

  components: {
     'TodoHeader' : TodoHeader,
     'TodoInput' : TodoInput,
     'TodoList' : TodoList,
     'TodoFooter' : TodoFooter,
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #CCEEFF;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style> 
