<template>
    <v-text-field
      v-model="searchInput"
      @input="onInput"
      placeholder="Поиск..."/>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    searchInput: {
      type: String,
      require: true,
      default: '',
    },
  },
  methods: {
    onInput() {
      this.$emit('onInput', this.searchInput);
    },
  },
};
</script>
