<template>
  <div class="collection todos">
    <div class="select">
      <label for="numbers">Filter Todos</label>
      <select name="numbers" v-model="selectedNumber">
        <option v-for="number in numbers" :key="number">{{ number }}</option>
      </select>
    </div>
    <div v-for="todo in filteredTodos" :key="todo.id">
      <TodoItem :todo="todo" />
    </div>
    <div class="pagination">
      <span>
        <a href="" v-if="startPageIndex > 0" @click.prevent="prevPage">Previous Page</a>
      </span>
      <span>
        <a
          href=""
          v-if="startPageIndex + parseInt(this.selectedNumber) < todos.length"
          @click.prevent="nextPage"
          >Next Page</a
        >
      </span>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  name: "Todos",
  props: ["todos"],
  components: {
    TodoItem,
  },
  data() {
    return {
      numbers: ["3", "5", "7"],
      selectedNumber: null,
      startPageIndex: 0,
    };
  },
  methods: {
    prevPage() {
      this.startPageIndex -= parseInt(this.selectedNumber);
      // console.log("selectedNumber_prevPage", this.selectedNumber);
      // console.log("startPageIndex_prevPage", this.startPageIndex);
    },
    nextPage() {
      this.startPageIndex += parseInt(this.selectedNumber);
      // console.log("selectedNumber_nextPage", this.selectedNumber);
      // console.log("startPageIndex_nextPage", this.startPageIndex);
    },
  },
  computed: {
    filteredTodos() {
      if (this.selectedNumber) {
        // console.log("selectedNumber_filter", this.selectedNumber);
        // console.log("startPageIndex_filter", this.startPageIndex);

        //slicar från: startPageIndex, till: (startPageIndex + selectedNumber)
        //slice utan tilldelning gör inget med arrayen
        return this.todos.slice(
          this.startPageIndex,
          this.startPageIndex + parseInt(this.selectedNumber)
        );
      } else {
        return this.todos;
      }
    },
  },
};
</script>

<style>
.todos {
  margin-bottom: 8rem;
  padding-bottom: 2rem;
}
.select {
  padding: 10px 20px;
}
select {
  display: block;
  width: 10rem;
}
.pagination {
  display: flex;
  justify-content: space-between;
}
.pagination span {
  padding: 30px 20px;
}
</style>
