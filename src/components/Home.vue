<template>
  <div id="app" class="container">
    <Header />
    <!-- <Todos :todos="todos" @toggle-completed="toggleCompleted" @del-todo="deleteTodo" />
    <AddTodo @add-todo="addTodo" /> -->
    <AddTodo @add-todo="addTodo" />
    <Todos :todos="todos" />
  </div>
</template>

<script>
import Header from "./Header";
import Todos from "./Todos";
import AddTodo from "./AddTodo";
//event bus
import { bus } from "../main";

export default {
  name: "Home",
  components: {
    Todos,
    Header,
    AddTodo,
  },
  data() {
    return {
      todos: [
        { content: "1 Walk with cats", id: 1, completed: false },
        { content: "2 Feed cats", id: 2, completed: false },
        { content: "3 Clean cats", id: 3, completed: false },
        { content: "4 Brush cats", id: 4, completed: false },
        { content: "5 Cuddle with cats", id: 5, completed: false },
        { content: "6 Walk with cats", id: 6, completed: false },
        { content: "7 Feed cats", id: 7, completed: false },
        { content: "8 Clean cats", id: 8, completed: false },
        { content: "9 Brush cats", id: 9, completed: false },
        { content: "10 Clean cats", id: 10, completed: false },
        { content: "11 Brush cats", id: 11, completed: false },
        { content: "12  Walk with cats", id: 12, completed: false },
      ],
    };
  },
  methods: {
    // toggleCompleted(id) {
    //   console.log("id", id);
    //   //loop the todos, check if same id, toggle completed
    //   this.todos.map((todo) => {
    //     if (todo.id === id) {
    //       todo.completed = !todo.completed;
    //     }
    //     return todo;
    //   });
    // },
    // deleteTodo(id) {
    //   console.log("id", id);
    //   //loop the todos, return only if not same id
    //   this.todos = this.todos.filter((todo) => {
    //     return todo.id !== id;
    //   });
    // },
    addTodo(content) {
      console.log("content", content);
      //make object
      const newTodo = {
        id: Math.random(),
        content: content,
        completed: false,
      };
      //make new array and add newTodo
      this.todos = [...this.todos, newTodo];
    },
  },

  created() {
    //toggle completed
    //listening to the toggle-completed event
    bus.$on("toggle-completed", (id) => {
      console.log("id", id);
      //take the passed in data and do something in this callback func
      //loop the todos, check if same id, toggle completed
      this.todos.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    });
    //delete todo
    //listening to the del-todo event
    bus.$on("del-todo", (id) => {
      console.log("id", id);
      //loop the todos, return only if not same id
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id;
      });
    });
  },
};
</script>

<style></style>
