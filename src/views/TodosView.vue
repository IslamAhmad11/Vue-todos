<script setup>
  import { ref, watch, computed } from "vue";
  import { uid } from "uid";
  import { Icon } from '@iconify/vue';
  import TodosCreator from "../components/TodosCreator.vue";
  import TodoItem from "@/components/TodoItem.vue";

  const todoList = ref([]);

  // chicking each one of todos is completed or not
  const todosCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

  // update todos within local storage
  watch(todoList, () => {
    setTodoListLocalStorage();
  },
  {
    // for tracking changes deep within todlist array
    deep: true,
  }
);

  const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};

  // Fetch Todo's on page load
  fetchTodoList();

  const setTodoListLocalStorage = () => {
    localStorage.setItem("todoList", JSON.stringify(todoList.value));
  };

  const createTodos = (myTodo) => {
    todoList.value.push({
      // using uid for generating a unique id for each task
      id: uid(),
      myTodo,
      isCompleted: null,
      isEditing: null,
    });
  };

  const toggleTodoComplete = (todoPos) => {
    todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
  };

  const toggleEditTodo = (todoPos) => {
    todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
  };

  const updateTodo = (todoVal, todoPos) => {
    todoList.value[todoPos].myTodo = todoVal;
  }

  const deleteTodo = (delTodoId) => {
    todoList.value = todoList.value.filter((delTodo) => delTodo.id !== delTodoId)
  }
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <!-- usin @ to call a custom emit from child component -->
    <TodosCreator @create-todo="createTodos" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem 
        v-for="(task, index) in todoList"
        :todoProp="task"
        :propIndex="index"
        @toggle-complete="toggleTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
    <!--when all of todos are completed we'll display a message-->
    <p v-if="todosCompleted && todoList.length > 0" class="todos-msg">
      <Icon icon="noto-v1:party-popper" />
      <span>You have completed all your todos!</span>
    </p>  
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
