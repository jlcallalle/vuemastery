<template>
  <div>
    <h1>Create Event - {{ $store.state.user.name }}</h1>
    <p>This event was created by  {{ user.name }} with id: {{ user.id }}</p>
    <ul>
      <li v-for="cat in categories" :key="cat"> {{ cat }}</li>
    </ul>
    <p>cantidad: {{ categories.length }} </p> 
    <p>Getter: Hay {{ catLength }} </p>
    <p>doneTodos {{ doneTodos  }}</p>
    <p>doneTodactiveTodosCountos {{ activeTodosCount  }}</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: {
    catLength() {
      //return this.$store.state.categories.length
      return this.$store.getters.catLength
    },
    doneTodos() {
      return this.$store.getters.doneTodos
    },
    activeTodosCount() {
      return this.$store.getters.activeTodosCount
    },
    ...mapState(['categories', 'user'])
  }
 /*  computed: mapState(['categories', 'user']) */
 
/*   computed: mapState ({
    user: 'user',
    categories: 'categories'
  }) */
/*   computed: mapState ({
    userName: state => state.user.name,
    userId: state => state.user.id,
    categories: state => state.categories
  }) */
/*   computed: {
    userName() {
      return this.$store.state.user.name
    },
    userId() {
      return this.$store.state.user.id
    }
  } */
}
</script>

<style scoped>
</style>
