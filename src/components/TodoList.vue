<template>
  <v-list class="list">
    <v-list-item-group color="primary">
      <TodoItem
        v-for="todo of todos"
        :todo="todo"
        :key="todo.id"
        @removeTodo="removeTodo"
        @changeData="changeData"
      />
    </v-list-item-group>
  </v-list>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  name: 'TodoList',
  components: {
    TodoItem,
  },
  props: {
    todos: {
      type: Array,
      require: true,
      default() {
        return [];
      },
    },
  },
  methods: {
    removeTodo(id) {
      this.$emit('removeTodo', id);
    },
    changeData(field, id) {
      this.$emit('changeData', field, id);
    },
  },
};
</script>

<style lang="scss" scoped>
.list {
  border: 1px solid rgba(0, 0, 0, 0.12);
  border-radius: 5px;
}
</style>
