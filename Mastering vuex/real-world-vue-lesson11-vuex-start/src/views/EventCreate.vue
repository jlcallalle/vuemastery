<template>
  <div>
    <h1>Create Event - {{ $store.state.user.name }}</h1>
    <p>This event was created by  {{ userName }} with id: {{ userId }}</p>
  </div>
</template>

<script>
export default {
  computed: {
    userName() {
      return this.$store.state.user.name
    },
    userId() {
      return this.$store.state.user.id
    }
  }
}
</script>

<style scoped>
</style>
