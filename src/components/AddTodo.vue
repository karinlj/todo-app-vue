<template>
  <div class="add_todo">
    <form @submit.prevent="$emit('add-todo', content)">
      <label for="">Add new Todo</label>
      <input type="text" v-model="content" placeholder="...add Todo" />
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",

  data() {
    return {
      content: "",
    };
  },
};
</script>

<style></style>
