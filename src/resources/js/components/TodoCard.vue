<template>
  <div :class="'card p-1 bc-inherit ' + className">
    <edit-todo-modal
      v-if="showEditForm"
      :todoData="todoData"
      :todoErrors="todoErrors"
      @editTodoHandler="editTodoHandler"
      @showEditFormHandler="showEditFormHandler"
    />
    <div class="d-flex" style="flex-wrap: wrap;">
      <h5 class="card-title p-2 mb-0" style="width: 60%;">{{ todoData.title }}</h5>
      <button class="ml-auto btn" style="width: 20%;" @click.prevent="showEditFormHandler">
        <svg
          class="bi bi-pencil-square"
          width="1em"
          height="1em"
          viewBox="0 0 16 16"
          fill="currentColor"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456l-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"
          />
          <path
            fill-rule="evenodd"
            d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"
          />
        </svg>
      </button>
      <button
        class="ml-auto btn"
        style="width: 20%;"
        @click.prevent="$emit('delTodoHandler', todoData.id)"
      >
        <svg
          class="bi bi-trash"
          width="1em"
          height="1em"
          viewBox="0 0 16 16"
          fill="currentColor"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"
          />
          <path
            fill-rule="evenodd"
            d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"
          />
        </svg>
      </button>
    </div>
    <p class="card-text p-2">{{ todoData.description }}</p>
    <div class="card-footer bg-transparent p-2">
      <button
        v-if="todoData.status == 1"
        class="btn bg-pale-orange btn-sm border-1px-bl"
        @click.prevent="moveTodoHandler(2)"
      >Move to In Progress</button>
      <button
        v-if="todoData.status == 2 || todoData.status == 3"
        class="btn bg-pale-red btn-sm border-1px-bl"
        @click.prevent="moveTodoHandler(1)"
      >Back to Todo</button>
      <button
        v-if="todoData.status == 2"
        class="btn bg-pale-green btn-sm border-1px-bl"
        @click.prevent="moveTodoHandler(3)"
      >Move to Done</button>
      <button
        v-if="todoData.status == 3"
        class="btn bg-pale-orange btn-sm border-1px-bl"
        @click.prevent="moveTodoHandler(2)"
      >Back to In Progress</button>
    </div>
  </div>
</template>

<script>
import EditTodoModal from "~/components/EditTodoModal";
import axios from "~/plugins/axios.js";

export default {
  props: {
    className: {
      type: String,
      default: ""
    },
    todoData: {
      type: Object,
      default: () => {
        return { message: "no data" };
      }
    }
  },

  components: {
    EditTodoModal
  },

  data() {
    return {
      showEditForm: false,
      todoErrors: null
    };
  },

  methods: {
    showEditFormHandler() {
      this.showEditForm = !this.showEditForm;
      this.todoErrors = null;
    },

    editTodoHandler(todo) {
      axios
        .put(`/api/todo/${this.todoData.id}`, { ...todo })
        .then(({ data }) => {
          this.todoData.title = todo.title;
          this.todoData.description = todo.description;
          this.showEditForm = false;
        })
        .catch(e => {
          console.log(e);
          this.todoErrors = e.response.data.errors;
        });
    },

    moveTodoHandler(status) {
      axios
        .put(`/api/todo/${this.todoData.id}`, { status: status })
        .then(({ data }) => {
          this.todoData.status = data.status;
        })
        .catch(e => {
          console.log(e);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.border-1px-bl {
  border: 1px solid black;
}
</style>
