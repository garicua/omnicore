<template>
  <div class="container">
    <Header>
      <div>
        <Button primary :text="'Добавить'"/>
        <Button primary :text="'Обновить'"/>
      </div>
    </Header>

    <CalendarNavigation>
      <Button secondary small @click="decreaseMonth" :text="'-'"/>
      <span class="calendar-navigation__text">{{months[month]}} {{year}}</span>
      <Button secondary small @click="increaseMonth" :text="'+'"/>
      <Button secondary small @click="resetMonth" :text="'Сегодня'"/>
    </CalendarNavigation>

    <CalendarBody :days-name="daysName" :calendar="calendar()"/>
  </div>
</template>

<script>
// @ is an alias to /src
import CalendarBody from '@/components/CalendarBody';
import CalendarNavigation from '@/components/CalendarNavigation';
import Button from '@/components/Button';
import Header from '@/components/Header';

export default {
  name: 'Calendar',
  data() {
    return {
      daysName: [],
      windowWidth: null,
      months: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Июль', 'Август', 'Сентябрь', 'Ноябрь', 'Декабрь'],
      data: new Date(),
      month: new Date().getMonth(),
      year: new Date().getFullYear(),
    };
  },
  components: {
    CalendarBody,
    CalendarNavigation,
    Button,
    Header,
  },
  methods: {
    decreaseMonth() {
      this.month--;
      if (this.month < 0) {
        this.month = 11;
        this.month--;
        this.year--;
      }
    },
    increaseMonth() {
      this.month++;
      if (this.month > 10) {
        this.month = -1;
        this.month++;
        this.year++;
      }
    },
    resetMonth() {
      this.month = new Date().getMonth();
      this.year = new Date().getFullYear();
    },
    calendar() {
      const days = [];
      let week = 0;
      days[week] = [];
      const lastMonthDay = new Date(this.year, this.month + 1, 0).getDate();
      for (let i = 1; i <= lastMonthDay; i++) {
        if (new Date(this.year, this.month, i).getDay() !== 1) {
          const a = { index: i };
          days[week].push(a);
          if (i === new Date().getDate() && this.year === new Date().getFullYear() && this.month === new Date().getMonth()) {
            a.current = '#c3c5dd';
          }
        } else {
          week++;

          days[week] = [];
          const a = { index: i };
          days[week].push(a);
        }
      }

      if (days[0].length > 0) {
        for (let i = days[0].length; i < 7; i++) {
          days[0].unshift('');
        }
      }
      if (days[days.length - 1].length > 0) {
        for (let i = days[days.length - 1].length; i < 7; i++) {
          days[days.length - 1].push('');
        }
      }
      return days;
    },
    updateWidth() {
      this.width = window.innerWidth;
      if (this.width < 1024) {
        this.daysName = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вск'];
      } else {
        this.daysName = ['Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота', 'Воскресенье'];
      }
    },
  },
  created() {
    window.addEventListener('resize', this.updateWidth);
    this.updateWidth();
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.updateWidth);
  },
};
</script>
