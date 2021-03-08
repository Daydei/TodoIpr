<template>
  <div class="header">
    <v-layout align-end justify-space-between>
      <h1 class="title">Todo List</h1>
      <div class="text">{{ countTodo.todoCount }} - задач, {{ countTodo.doneCount }} завершено</div>
    </v-layout>
    <v-divider />
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    countTodo: {
      type: Object,
      require: true,
      default() {
        return {
          todoCount: 0,
          doneCount: 0,
        };
      },
    },
  },
};
</script>

<style scoped>
.header {
  margin-bottom: 20px;
}
</style>
