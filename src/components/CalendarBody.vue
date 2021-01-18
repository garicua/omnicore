<template>
  <div class="calendar-body">
    <div class="calendar-body__text">
      <p>Для просмотра событий поверните экран в альбомный вид</p>
    </div>
    <ul class="calendar-body__days">
      <li v-for="day in daysName"
          :key="day"
          class="calendar-body__list">
        {{ day }}
      </li>
    </ul>
    <ul v-for="(week, index) in calendar" :key="index" class="calendar-body__week">
      <li v-for="(day, ind) in week" :key="ind"
          :style="{'background-color': day.current}"
          :class="{'calendar-body__day-colored': getPost(day)}"
          class="calendar-body__day"
          @click="click(day, $event)"
      >
           <span class="calendar-body__body" v-if="getPost(day)">
            <span class="calendar-body__body-item">{{ getPost(day).userEvent }}</span>
            <span class="calendar-body__body-item">{{ getPost(day).userParticipant }}</span>
            <span class="calendar-body__body-item">{{ getPost(day).userDescription }}</span>
          </span>
        <span class="calendar-body__date">{{ day.index }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "CalendarBody",
  props: {
    daysName: Array,
    calendar: Array,
    userEvent: String,
    userParticipant: String,
    userDescription: String,
    posts: {}
  },
  methods: {
    getPost(day) {
      const id = `${day.index}-${day.month}-${day.year}`;
      if (typeof this.posts[id] !== 'undefined') {
        return this.posts[id];
      }

      return null;
    },
    click(day) {
      if (day) {
        this.$emit('click', `${day.index}-${day.month}-${day.year}`);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/calendar-body";
</style>
