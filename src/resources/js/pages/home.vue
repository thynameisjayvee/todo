<template>
  <div class="row">
    <div class="col-md-4">
      <div class="wrapper bg-pale-red mx-1">
        <h4 class="p-2">Todo</h4>
        <ul class="list-group">
          <li class="list-group-item">
            <todo-card class="bg-pale-red" />
          </li>
          <li class="list-group-item">
            <todo-card class="bg-pale-red" />
          </li>
        </ul>
      </div>
    </div>
    <div class="col-md-4">
      <div class="wrapper bg-pale-orange mx-1">
        <h4 class="p-2">In Progress</h4>
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
        <h4 class="p-2">Done</h4>
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

export default {
  middleware: "auth",

  metaInfo() {
    return { title: this.$t("home") };
  },

  components: {
    TodoCard
  },

  data: () => {
    return {};
  }
};
</script>

<style lang="scss" scoped>
.list-group-item {
  background-color: inherit;
}
</style>
