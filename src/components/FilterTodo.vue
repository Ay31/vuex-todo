<template>
  <div class="filter">
      <span>Filter Todo</span>
      <select @change="onFilter($event)">
          <option value="200">200</option>
          <option value="100">100</option>
          <option value="50">50</option>
          <option value="20">20</option>
          <option value="5">5</option>
      </select>
  </div>
</template>

<script>
import { mapActions } from "vuex"
export default {
    name:"FilterTodo",
    methods: {
        ...mapActions(["filterTodo"]),
        onFilter(event) {
            this.filterTodo(event)
        }
    }
}
</script>

<style scoped>
    .filter {
        margin-top:10px;
    }
</style>