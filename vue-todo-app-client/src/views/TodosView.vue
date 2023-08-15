<script setup>
  import { reactive, watch, computed } from 'vue';
  import TodoCreator from '../components/TodoCreator.vue';
  import { uid } from 'uid';
  import TodoItem from '../components/TodoItem.vue';
  import { Icon } from '@iconify/vue';

  const todoList = reactive([])

  watch(todoList, () => {
    setTodoListLocalStorage(); //same as the useEffect in react
  }, {
    deep: true
  })

  const todoCompleted = computed(() => {
    return todoList.every((eachTodo) => eachTodo.isCompleted);
  })

  const setTodoListLocalStorage = () => {
    localStorage.setItem("todoList", JSON.stringify(todoList));
  };

  const fetchTodoList = () => {
    const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
    if (savedTodoList) {
      todoList.splice(0, todoList.length, ...savedTodoList);
    }
  }

  fetchTodoList()

  const createTodo = (todo) => {
    todoList.push({
      id: uid(),
      todo,
      isCompleted: false,
      isEditing: false,
    })
  }

  const toggleTodoComplete = (todoPos) => {
    todoList[todoPos].isCompleted = !todoList[todoPos].isCompleted;
  }

  const toggleEditTodo = (todoPos) => {
    todoList[todoPos].isEditing = !todoList[todoPos].isEditing; 
  }

  const updateTodo = (todoPos, todoVal) => {
    todoList[todoPos].todo = todoVal;
  }

  const deleteTodo = (todoId) => {
    //because we create todoList using the 'reactive' way, we can reassign the whole todoList.
    //so we need to find the position of matching index and splice it.
    const index = todoList.findIndex((todo) => todo.id === todoId);
    if (index !== -1) {
      todoList.splice(index, 1);
    }
    setTodoListLocalStorage() 
  }

</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo"/>
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem 
        v-for="(todo, index) in todoList" 
        :todo="todo" 
        :index="index" 
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @updated-todo="updateTodo"
        @delete-todo="deleteTodo(todo.id)"
      />
    </ul>
    <p v-else class="todo-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" color="green" width="22" height="22" />
      <span>You have no todos to complete! Add one!</span>
    </p>
    <p v-if="todoCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have completed all your todos!</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

</style>
