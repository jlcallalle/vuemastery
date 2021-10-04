<template>
  <div>
    <h1>Create Event - {{ $store.state.user.name }}</h1>
    <p>This event was created by  {{ user.name }} with id: {{ user.id }}</p>
    <p><strong>Ejemplo Array Categorias</strong></p>
    <ul>
      <li v-for="cat in categories" :key="cat"> {{ cat }}</li>
    </ul>
    <p>cantidad: {{ categories.length }} </p> 
    <p>Getter: Hay {{ catLength }} </p>
    <p><strong>Ejemplo Array Todos</strong></p>
    <p>doneTodos {{ doneTodos  }}</p>
    <p>doneTodactiveTodosCountos {{ activeTodosCount  }}</p>
    <p><strong>Getters Dinámico</strong></p>
    <!-- <p>{{ getEvent(1) }} </p> -->
    <p>{{ getEventById(1) }} </p>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { mapGetters } from 'vuex'


export default {
  computed: {
     ...mapGetters(['getEventById']),
     /* getEvent() {
      return this.$store.getters.getEventById
    }, */
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
