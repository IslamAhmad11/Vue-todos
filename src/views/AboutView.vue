<template>
  <div class="about">
    <h1>Vue Todos</h1>
    <p>
      Vue Todos is a CRUD Todo tracking application Track your daily task's using this todo tracker with abilities to save, complete, edit & delete todos.
      Feel free to add on to this application with functionalities such as the ability to drag and reorder todos, animate creation/deletion of todos or
      even create this into a full stack application with the ability to have different lists for different days of tracking todos!</p>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
.about{
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  align-items: start;
  flex-direction: column;
  padding: 25px 16px;
  line-height: 30px;
}
h1{margin-bottom: 20px;}
</style>
