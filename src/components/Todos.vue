<template>
  <div>
      <h3>Todos</h3>
      <div class="legend">
        <span>Double Click to mark as complete</span>
        <span>
          <span class="incomplete-box"></span> = Incomplete
        </span>
        <span>
          <span class="complete-box"></span> = Complete
        </span>
      </div>
    <div class="todos">
      <div
      @dblclick="onDblClick(todo)" 
      v-for="todo of allTodos" 
      :key="todo.id"
      :class="{'is-complete':todo.completed}" 
      class="todo">
      {{ todo.title }}
      <i class="fa fa-trash" @click="deleteTodo(todo.id)"></i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters,mapActions } from "vuex"

export default {
  name: "Todos",
  methods: {
    ...mapActions(["fetchTodos","deleteTodo","updateTodo"]),
    onDblClick(todo) {
      const newTodo = {
        id: todo.id,
        title: todo.title,
        userId: todo.userId,
        completed: !todo.completed
      }
      this.updateTodo(newTodo)
    }

  },
  computed: {
    ...mapGetters(["allTodos"])
  },
  created() {
      this.fetchTodos()
  }
};
</script>

<style scoped>
.todos {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-gap: 1em;
}

.todo {
    border: 1px solid #ccc;
    background: #41b88c;
    padding: 1rem;
    border-radius: 5px;
    text-align: center;
    position: relative;
    cursor: pointer;
    user-select:none;
}

i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #fff;
  cursor: pointer;
}

.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #3CB371;
}

.incomplete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #41b883;
}

.is-complete {
  background: #3CB371;
  color:#fff;
}

@media (max-width: 500px) {
  .todos {
    grid-template-columns: 1fr;
  }
}
</style>