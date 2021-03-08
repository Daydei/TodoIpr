<template>
  <v-app>
    <v-container class="wrapper">
      <Header
        :countTodo="countTodo"/>
      <v-layout justify-space-between>
        <SearchInput
          :searchInput="searchInput"
          @onInput="onInput"/>
        <FilterApp
          :filter="filter"
          @changeFilter="changeFilter"/>
      </v-layout>
      <TodoList
        v-if="filtredItems.length !== 0"
        :todos="filtredItems"
        @removeTodo="removeTodo"
        @changeData="changeData"/>
      <p
        v-else
        class="text">Нет задач</p>
      <AddTodo
        @addTodoItem="addTodoItem" />
    </v-container>
  </v-app>
</template>

<script>
import Header from './components/Header.vue';
import SearchInput from './components/SearchInput.vue';
import FilterApp from './components/FilterApp.vue';
import TodoList from './components/TodoList.vue';
import AddTodo from './components/AddTodo.vue';

export default {
  name: 'App',
  components: {
    Header,
    SearchInput,
    FilterApp,
    TodoList,
    AddTodo,
  },
  data: () => ({
    todoData: [],
    searchInput: '',
    filter: 'all',
  }),
  methods: {
    onInput(searchInput) {
      this.searchInput = searchInput;
    },
    changeFilter(value) {
      this.filter = value;
    },
    filterItems(items, filter) {
      switch (filter) {
        case 'all':
          return items;
        case 'active':
          return items.filter((item) => !item.done);
        case 'done':
          return items.filter((item) => item.done);
        default:
          return items;
      }
    },
    changeData(field, id) {
      const index = this.todoData.findIndex((item) => item.id === id);
      this.todoData[index][field] = !this.todoData[index][field];
      this.saveTodo();
    },
    createTodo(label) {
      const newId = Date.now();
      return {
        label,
        important: false,
        done: false,
        id: newId,
      };
    },
    addTodoItem(label) {
      const newItem = this.createTodo(label);
      this.todoData.push(newItem);
      this.saveTodo();
    },
    saveTodo() {
      const parsed = JSON.stringify(this.todoData);
      localStorage.setItem('todoData', parsed);
    },
    removeTodo(id) {
      this.todoData = this.todoData.filter((item) => item.id !== id);
      this.saveTodo();
    },
  },
  computed: {
    filtredItems() {
      const actualaItems = this.todoData.filter((item) => item.label
        .toLowerCase()
        .indexOf(this.searchInput.toLowerCase()) > -1);
      return this.filterItems(actualaItems, this.filter);
    },
    countTodo() {
      const doneCount = this.todoData.filter((item) => item.done).length;
      const todoCount = this.todoData.length - doneCount;
      return {
        todoCount,
        doneCount,
      };
    },
  },
  mounted() {
    if (localStorage.getItem('todoData')) {
      try {
        this.todoData = JSON.parse(localStorage.getItem('todoData'));
      } catch (e) {
        localStorage.removeItem('todoData');
      }
    }
  },
};
</script>

<style scoped>
.wrapper {
  max-width: 417px;
  padding-top: 50px;
}
.text {
  border-radius: 5px;
  box-shadow: 0px 0px 0px 0px rgb(0 0 0 / 20%),
              0px 0px 0px 0px rgb(0 0 0 / 14%),
              0px 0px 0px 0px rgb(0 0 0 / 12%);
  border: 1px solid rgba(0, 0, 0, 0.12);
  padding: 8px 16px;
  font-size: 16px;
}
</style>
