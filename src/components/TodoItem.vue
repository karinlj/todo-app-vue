<template>
  <div class="collection-item" :class="{ is_completed: todo.completed }">
    <!-- <div class="item">
      <input type="checkbox" @change="$emit('toggle-completed', todo.id)" />
      <p class="todoItem_content">{{ todo.content }}</p>
      <button @click="$emit('del-todo', todo.id)">
        x
      </button>
    </div> -->
    <div class="item">
      <input type="checkbox" @change="toggleCompleted" />
      <p class="todoItem_content">{{ todo.content }}</p>
      <button @click="deleteTodo">
        x
      </button>
    </div>
  </div>
</template>

<script>
import { bus } from "../main";

export default {
  name: "TodoItem",
  props: ["todo"],
  data() {
    return {};
  },
  methods: {
    toggleCompleted() {
      //emit custom event on the bus, add key
      bus.$emit("toggle-completed", this.todo.id);
    },
    deleteTodo() {
      //emit custom event on the bus, add key
      bus.$emit("del-todo", this.todo.id);
    },
  },
};
</script>

<style scoped>
.is_completed {
  text-decoration: line-through;
}
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
button {
  color: #fff;
  background: #f44336;
  border-radius: 4px;
  border: none;
  padding: 5px 9px;
  cursor: pointer;
  line-height: 1;
  font-size: 17px;
}
[type="checkbox"]:not(:checked),
[type="checkbox"]:checked {
  opacity: 1;
  pointer-events: all;
  display: inline-block;
}
.todoItem_content {
  padding-left: 2rem;
}
</style>
