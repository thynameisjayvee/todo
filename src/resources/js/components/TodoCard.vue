<template>
  <div :class="'card p-1 bc-inherit ' + className">
    <h5 class="card-title">{{ title }}</h5>
    <p class="card-text">{{ description }}</p>
  </div>
</template>

<script>
export default {
  props: {
    className: {
      type: String,
      default: ""
    },
    title: {
      type: String,
      default: "Insert Title Here"
    },
    description: {
      type: String,
      default: "Insert Description Here"
    }
  }
};
</script>

<style>
</style>
