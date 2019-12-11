<template>
  <div class="container">
    <h1>
      Nuxt.js Advent Calendar 2019
    </h1>

    <p>{{ comment }}</p>

    <div class="calendar">
      <a-card
        v-for="dayName in dayNames"
        :key="dayName"
        :title="dayName"
      ></a-card>

      <a-card
        v-for="day in days"
        :key="day.date"
        :title="day.date"
      >
        <a-card-meta>
          <a-avatar
            slot="avatar"
            :src="day.authorImageUrl"
            :alt="day.authorName"
          />
        </a-card-meta>

        <a
          :href="`https://qiita.com/${day.authorName}`"
          target="_blank"
          rel="noopener noreferrer"
          class="author-name ellipsis"
        >
          {{ day.authorName }}
        </a>

        <a v-if="day.articleUrl !== null"
          :href="day.articleUrl"
          target="_blank"
          rel="noopener noreferrer"
        >
          {{ day.comment }}
        </a>

        <p v-else>
          {{ day.comment }}
        </p>
      </a-card>

      <a-card
        v-for="day in [26, 27, 28]"
        :key="day"
        :title="day"
      ></a-card>
    </div>

    <p class="notice">
      ※ このページはレスポンシブ対応していません。デスクトップサイズの画面でご覧ください。
    </p>
  </div>
</template>

<script>
import { parse } from 'node-html-parser'

export default {
  async asyncData({ $axios }) {
    const { data } = await $axios.get('https://qiita.com/advent-calendar/2019/nuxt-js')
    const root = parse(data)
    return {
      comment: root.querySelector('.markdownContent').text,
      dayNames: root.querySelectorAll('.adventCalendarCalendar_dayName').map(dayName => dayName.text),
      days: root.querySelectorAll('.adventCalendarCalendar_day').map(day => {
        const articleUrl = day.querySelector('.adventCalendarCalendar_comment').querySelector('a') ?
          day.querySelector('.adventCalendarCalendar_comment').querySelector('a').attributes['href'] :
          null
        return {
          date: day.querySelector('.adventCalendarCalendar_date').text,
          authorName: day.querySelector('.adventCalendarCalendar_author').text.replace(/\s|&nbsp;/g, ''),
          authorImageUrl: day.querySelector('.adventCalendarCalendar_authorIcon').attributes['src'],
          comment: day.querySelector('.adventCalendarCalendar_comment').text,
          articleUrl: articleUrl
        }
      })
    }
  }
}
</script>

<style>
.container {
  padding: 5%;
}

.calendar {
  display: flex;
  flex-wrap: wrap;
  border: 1px solid #e8e8e8;
}

.calendar > .ant-card {
  width: calc(100% / 7);
  min-width: 120px;
  border-radius: 0;
}

.calendar .author-name {
  display: block;
  padding: 10px 0 20px;
  margin-bottom: 20px;
  border-bottom: 1px solid #e8e8e8;
}

.notice {
  padding: 20px 0;
}
</style>
