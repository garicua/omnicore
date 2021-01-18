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
      <li v-for="(day, ind) in week" :key="ind"
          :style="{'background-color': day.current}"
          class="calendar-body__day"
          v-on="$listeners"
      >
        <span class="calendar-body__body">
          <span class="calendar-body__body-item">{{ userEvent }}</span>
          <span class="calendar-body__body-item">{{ userParticipant }}</span>
          <span class="calendar-body__body-item">{{ userDescription }}</span>
        </span>
        <span class="calendar-body__date" ref="${{day.index}}">{{ day.index }}</span>

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
  }
}
</script>

<style lang="scss" scoped>
  @import "@/assets/style/components/calendar-body";
</style>
