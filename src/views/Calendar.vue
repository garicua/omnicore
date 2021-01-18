<template>
  <div class="container">
    <Header>
      <div>
        <Button primary :text="'Обновить'"  @click="resetMonth"/>
      </div>
    </Header>

    <CalendarNavigation>
      <Button secondary small @click="decreaseMonth" :text="'-'"/>
      <span class="calendar-navigation__text">{{months[month]}} {{year}}</span>
      <Button secondary small @click="increaseMonth" :text="'+'"/>
      <Button secondary small @click="resetMonth" :text="'Сегодня'"/>
    </CalendarNavigation>

    <CalendarBody :days-name="daysName"
                  :calendar="calendar()"
                  :posts="posts"
                  @click="toggleEventModal($event)"
    />
    <transition name="fade">
      <AddEvent v-if="isOpenEventModal"
                :data="dayId"
                @click="toggleEventModal($event)"
      >
        <form @submit.prevent="submitHandler" ref="form">
          <InputText :placeholder="'Событие'"
                     v-model="userEvent"
          />
          <InputText :placeholder="'Учасники'"
                     v-model="userParticipant"
          />
          <label for="userDescription"></label>
          <textarea v-model="userDescription"
                    id="userDescription"
                    placeholder="'Введите описания события'"
                    class="textarea"/>
          <Button secondary small :text="'Готово'" :type-btn="'submit'"/>
          <Button secondary small ml :text="'Удалить'" @click="clearUserPost"/>
        </form>
      </AddEvent>
    </transition>
  </div>
</template>

<script>
import CalendarBody from '@/components/CalendarBody';
import CalendarNavigation from '@/components/CalendarNavigation';
import Button from '@/components/Button';
import Header from '@/components/Header';
import AddEvent from '@/components/AddEvent';
import InputText from '@/components/InputText';

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
      userEvent: '',
      userParticipant: '',
      userDescription: '',
      isOpenEventModal: false,
      dayId: null,
      posts: {
        '31-1-2021': {userDescription: "last day of January", userEvent: "GYM day", userParticipant: "Alex",},
        '7-1-2021': {userDescription: "family meetup", userEvent: "Christmas day", userParticipant: "all",}
      },
    };
  },
  components: {
    CalendarBody,
    CalendarNavigation,
    Button,
    Header,
    AddEvent,
    InputText,
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
          const a = { index: i, year: this.year, month: this.month + 1 };
          days[week].push(a);
          if (i === new Date().getDate() && this.year === new Date().getFullYear() && this.month === new Date().getMonth()) {
            a.current = '#c3c5dd';
          }
        } else {
          week++;
          days[week] = [];
          const a = { index: i, year: this.year, month: this.month + 1};
          days[week].push(a);
          if (i === new Date().getDate() && this.year === new Date().getFullYear() && this.month === new Date().getMonth()) {
            a.current = '#c3c5dd';
          }
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
    toggleEventModal(event){
      this.isOpenEventModal = !this.isOpenEventModal;
      if(event){
        this.dayId = event
      }
    },
    submitHandler() {
      this.posts[this.dayId] = {
        userEvent: this.userEvent,
        userParticipant: this.userParticipant,
        userDescription: this.userDescription,
      }
      this.isOpenEventModal = false;
      this.$refs.form.reset()
      console.log(this.posts);
    },
    clearUserPost(){
      this.posts[this.dayId] = null;
      this.isOpenEventModal = false;
    }
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

<style lang="scss" >
  .textarea {
    display: block;
    width: 100%;
    min-height: 100px;
    padding: 10px 16px 8px;
    margin-bottom: 12px;
    background-color: #fff;
    font-size: 14px;
    color: #000;
    box-shadow: 0 4px 8px rgba(0,0,0,.9);
  }
</style>
