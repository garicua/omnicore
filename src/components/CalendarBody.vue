<template>
  <div class="calendar-body">
    <ul class="calendar-body__days">
      <li v-for="day in daysName"
          :key="day"
          class="calendar-body__list">
        {{ day }}
      </li>
    </ul>
    <ul v-for="(week, index) in calendar" :key="index" class="calendar-body__week">
      <li v-for="(day, index) in week" :key="index"
          :style="{'background-color': day.current}"
          class="calendar-body__week"
      >
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
  }
}
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/calendar-body";
</style>
