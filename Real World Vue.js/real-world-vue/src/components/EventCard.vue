<template>
  <router-link class="event-link" :to="{ name: 'event-show', params: { id: event.id } }">
    <div class="event-card -shadow">
      <span class="eyebrow">@{{ event.time }} on {{ event.date }}</span>
      <h4 class="title">{{ event.title }}</h4>
      <BaseIcon name="users">{{ event.attendees.length }} attending
        <!-- <template slot="test">
          <span> - slot test</span>
        </template> -->
      </BaseIcon>
      
    </div>
  </router-link>
</template>

<script>
export default {
  props: {
    event: Object
  }
  // data() {
  //   return {
  //     title: 'Beach Cleanup',
  //     event: {
  //       id: 1,
  //       title: 'Bearch Cleanup',
  //       date: 'Tues Aug 19, 2018',
  //       time: '6:00',
  //       attendees: [
  //         { id: 'aaaaa', name: 'Adam Jahr' },
  //         { id: 'bbbbb', name: 'Grep Polar' }
  //       ]
  //     }
  //   }
  // }
}
</script>

<style scoped>
.event-card {
  padding: 20px;
  margin-bottom: 24px;
  transition: all 0.2s linear;
  cursor: pointer;
}
.event-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2), 0 1px 15px 0 rgba(0, 0, 0, 0.19);
}
.event-card > .title {
  margin: 0;
}
.event-link {
  color: black;
  text-decoration: none;
  font-weight: 100;
}
</style>
