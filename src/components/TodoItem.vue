<template>
  <v-list-item :class="{important: todo.important}">
    <v-layout align-center justify-space-between>
      <v-layout align-center>
        <v-checkbox
          v-model="checkbox"
          @change="changeData('done')"
        ></v-checkbox>
        <span :class="{through: checkbox}">{{ todo.label }}</span>
      </v-layout>
      <v-btn @click="changeData('important')">
        <v-icon>
          mdi-exclamation-thick
        </v-icon>
      </v-btn>
      <v-btn @click="removeTodo">
        <v-icon>
          mdi-delete
        </v-icon>
      </v-btn>
    </v-layout>
  </v-list-item>
</template>

<script>
export default {
  name: 'TodoItem',
  data() {
    return {
      checkbox: false,
    };
  },
  mounted() {
    if (this.todo.done !== this.checkbox) {
      this.checkbox = this.todo.done;
    }
  },
  props: {
    todo: {
      type: Object,
      require: true,
      default() {
        return {
          label: '',
          important: false,
          done: false,
          id: 0,
        };
      },
    },
  },
  methods: {
    removeTodo() {
      this.$emit('removeTodo', this.todo.id);
    },
    changeData(field) {
      this.$emit('changeData', field, this.todo.id);
    },
  },
};
</script>

<style lang="scss" scoped>
.through {
  text-decoration: line-through;
}
.important {
  font-weight: bold;
}
</style>
