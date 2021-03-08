<template>
  <v-btn-toggle color="deep-purple accent-3">
    <v-btn
      value="all"
      @click="changeFilter('all')"
      :class="{'active-btn': filter === 'all'}">
      All
    </v-btn>
    <v-btn
      value="active"
      @click="changeFilter('active')"
      :class="{'active-btn': filter === 'active'}">
      Active
    </v-btn>
    <v-btn
      @click="changeFilter('done')"
      :class="{'active-btn': filter === 'done'}">
      Done
    </v-btn>
  </v-btn-toggle>
</template>

<script>
export default {
  props: {
    filter: {
      type: String,
      require: true,
      default: 'all',
    },
  },
  methods: {
    changeFilter(value) {
      this.$emit('changeFilter', value);
    },
  },
};
</script>

<style scoped>
.active-btn{
  color: inherit !important;
  opacity: 1;
}
.active-btn:before{
  opacity: 0.18;
}
</style>
