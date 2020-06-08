<template>
  <div id="backshadow" class="wrapper">
    <div class="card" style="width: 420px;">
      <div class="card-header">Edit Todo</div>
      <div class="card-body">
        <form>
          <div class="form-group">
            <label for="title">Title</label>
            <input v-model="todo.title" name="title" type="text" class="form-control" />
            <small
              v-if="todoErrors && todoErrors.title"
              class="form-text"
              style="color: red;"
            >{{ todoErrors.title[0] }}</small>
          </div>
          <div class="form-group">
            <label for="description">Description</label>
            <textarea
              v-model="todo.description"
              class="form-control"
              rows="5"
              style="resize: none;"
            />
            <small
              v-if="todoErrors && todoErrors.description"
              class="form-text"
              style="color: red;"
            >{{ todoErrors.description[0] }}</small>
            <!-- <input type="description" class="form-control" /> -->
          </div>
          <button class="btn btn-primary" @click.prevent="$emit('editTodoHandler', todo)">Save</button>
          <button class="btn btn-secondary" @click.prevent="$emit('showEditFormHandler')">Cancel</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todoErrors: {
      type: Object,
      default: () => {
        return { message: "no data" };
      }
    },
    todoData: {
      type: Object,
      default: () => {
        return { message: "no data" };
      }
    }
  },

  data() {
    return {
      todo: {
        title: "",
        description: ""
      }
    };
  },

  mounted() {
    this.todo.title = this.todoData.title;
    this.todo.description = this.todoData.description;
    this.$root.$el.append(this.$el);
  }
};
</script>

<style lang="scss" scoped>
.wrapper {
  height: 100%;
  position: absolute;
  top: 0;
  width: 100%;
  background: rgb(0, 0, 0, 0.5);
  .card {
    width: 420px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}
</style>
