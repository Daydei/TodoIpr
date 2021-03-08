<template>
  <form
    @submit="addTodoItem">
    <v-layout align-center justify-space-between>
      <v-text-field
        v-model="addInput"
        placeholder="Что нужно сделать?"
        class="input"/>
      <v-btn
        @click="addTodoItem">
        Добавить
      </v-btn>
    </v-layout>
  </form>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      addInput: '',
    };
  },
  methods: {
    addTodoItem() {
      this.$emit('addTodoItem', this.addInput);
      this.addInput = '';
    },
  },
};
</script>

<style lang="scss" scoped>
.input {
  margin-right: 10px;
}
</style>
