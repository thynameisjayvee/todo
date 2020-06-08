<template>
  <div class="row">
    <todo-modal
      v-if="showForm"
      @showFormHandler="showFormHandler"
      @addTodoHandler="addTodoHandler"
    />
    <div class="col-md-4">
      <div class="wrapper bg-pale-red mx-1">
        <div class="d-flex">
          <h4 class="p-2 mb-0">Todo</h4>
          <button class="ml-auto btn" @click="showFormHandler">
            <svg
              class="bi bi-plus-circle"
              width="1em"
              height="1em"
              viewBox="0 0 16 16"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M8 3.5a.5.5 0 0 1 .5.5v4a.5.5 0 0 1-.5.5H4a.5.5 0 0 1 0-1h3.5V4a.5.5 0 0 1 .5-.5z"
              />
              <path
                fill-rule="evenodd"
                d="M7.5 8a.5.5 0 0 1 .5-.5h4a.5.5 0 0 1 0 1H8.5V12a.5.5 0 0 1-1 0V8z"
              />
              <path
                fill-rule="evenodd"
                d="M8 15A7 7 0 1 0 8 1a7 7 0 0 0 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"
              />
            </svg>
          </button>
        </div>
        <ul class="list-group">
          <li v-for="(todoData, index) in todos" :key="index" class="list-group-item">
            <todo-card class="bg-pale-red" :todoData="todoData" />
          </li>
          <!-- <li class="list-group-item">
            <todo-card class="bg-pale-red" />
          </li>-->
        </ul>
      </div>
    </div>
    <div class="col-md-4">
      <div class="wrapper bg-pale-orange mx-1">
        <h4 class="p-2 mb-0">In Progress</h4>
        <ul class="list-group">
          <li class="list-group-item">
            <todo-card class="bg-pale-orange" />
          </li>
          <li class="list-group-item">
            <todo-card class="bg-pale-orange" />
          </li>
        </ul>
      </div>
    </div>
    <div class="col-md-4">
      <div class="wrapper bg-pale-green mx-1">
        <h4 class="p-2 mb-0">Done</h4>
        <ul class="list-group">
          <li class="list-group-item">
            <todo-card class="bg-pale-green" />
          </li>
          <li class="list-group-item">
            <todo-card class="bg-pale-green" />
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import TodoCard from "~/components/TodoCard";
import TodoModal from "~/components/TodoModal";
import axios from "~/plugins/axios.js";

export default {
  middleware: "auth",

  metaInfo() {
    return { title: this.$t("home") };
  },

  components: {
    TodoCard,
    TodoModal
  },

  data: () => {
    return {
      showForm: false,
      todos: null
    };
  },

  methods: {
    fetchTodosHandler() {
      axios
        .get("/api/todo")
        .then(({ data }) => {
          this.todos = data;
        })
        .catch(e => {
          console.log(e);
        });
    },

    showFormHandler() {
      this.showForm = !this.showForm;
    },

    addTodoHandler(todo) {
      axios
        .post("/api/todo", { ...todo })
        .then(res => {
          console.log(res);
        })
        .catch(e => {
          console.log(e);
        });
    }
  },

  created() {
    this.fetchTodosHandler();
  }
};
</script>

<style lang="scss" scoped>
.list-group-item {
  background-color: inherit;
}
</style>
