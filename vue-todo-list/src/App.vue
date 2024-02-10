<!-- App.vue -->
<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h2 {
  color: #42b983;
}
</style>
