<script setup>
  import { ref } from "vue";
  import { uid } from "uid";
  import TodosCreator from "../components/TodosCreator.vue";
  const todoList = ref([]);

  const createTodos = (myTodo) => {
    todoList.value.push({
      // using uid for generating a unique id for each task
      id: uid(),
      myTodo,
      isCompleted: null,
      isEditing: null,
    });
  };
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <!-- usin @ to call a custom emit from child component -->
    <TodosCreator @create-todo="createTodos" />
  </main>
</template>

<style lang="scss" scoped>
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
  }
</style>
