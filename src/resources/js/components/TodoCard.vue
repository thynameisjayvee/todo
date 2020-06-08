<template>
  <div :class="'card p-1 bc-inherit ' + className">
    <h5 class="card-title">{{ todoData.title }}</h5>
    <p class="card-text">{{ todoData.description }}</p>
  </div>
</template>

<script>
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
  }
};
</script>

<style>
</style>
