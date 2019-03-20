<template>
  <article class="wrap">
    <section>
      <div>
        url:
        <input nam="url" />
        <button>copy</button>
      </div>
      <div>
        사용자:
        <label>test</label>
      </div>
    </section>
    <section class="calendar-wrap">
      <div class="calendar">
      </div>
      <div class="calendar">
        <!--ul*6>li.day$*7>button[click="toggleDay"]-->
        <ul>
          <li class="day1">Sun</li>
          <li class="day2">Mon</li>
          <li class="day3">Tue</li>
          <li class="day4">Wed</li>
          <li class="day5">Thu</li>
          <li class="day6">Fri</li>
          <li class="day7">Sat</li>
        </ul>
        <ul v-for="weeks in 6" :key="weeks">
          <li v-for="dayinweek in 7"
          :key="dayinweek">
            <day></day>
          </li>
        </ul>
      </div>
      <div class="calendar"></div>
    </section>
    <section>
      <div>
        참여자:
      </div>
      <div>
        총 0명
      </div>
    </section>
  </article>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Day from "../components/calendar/Day";

export default {
  components: {
    Day,
    Logo
  }
}
</script>

<style lang="scss">

html, body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

ul, li {
  list-style: none;
  margin: 0;
  padding: 0;
}

article {
  height: 100%;
  display: flex;
  flex-direction: column;
}

section {
  flex: 1;
  border: 1px solid red;

  &.calendar-wrap {
    height: 400px;
    display: flex;

    .calendar {
      flex: 1;
      display: flex;
      flex-direction: column;

      ul {
        flex: 1;
        display: flex;

        li {
          flex: 1;
          border: 1px solid red;
        }
      }
    }
  }
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
