<template>
  <div>
    <!--<img src="./imgs/dragonflies.jpg" />-->
    <h2>Fall 2021 Season Start</h2>
    <p>I hope all have had an awesome summer!</p>
    <p>I'm excited to have the girls on our team and we've had a chance to have a couple of morning practices. I'd like to have our next practice on Monday morning and then invite everyone for a team pizza party and to vote on our team name Wednesday evening! It will be a great chance for parents to get to know each other, as well. We have our first game coming up quickly on Saturday, August 21st. To help track practices and games, I've make a calendar below for your convenience.</p>
    <p>We'll start warming up 15 minutes before game time. So if the game is 12:30 pm, we'll start kicking the ball around and doing stretches at 12:15pm. I'll bring the soccer balls and usually be wearing my orange hat, so you can find us easily.</p>
    <p>See everyone next week!</p>
    </p>
        <div class="calendar-parent">
            <calendar-view
                :events="events"
                :show-date="showDate"
                :time-format-options="{hour: 'numeric', minute:'2-digit'}"
                :enable-drag-drop="true"
                eventContentHeight="5.5em"
                :disable-past="disablePast"
                :disable-future="disableFuture"
                :show-event-times="showEventTimes"
                :display-period-uom="displayPeriodUom"
                :display-period-count="displayPeriodCount"
                :starting-day-of-week="startingDayOfWeek"
                :class="themeClasses"
                :period-changed-callback="periodChanged"
                :current-period-label="useTodayIcons ? 'icons' : ''"
                @drop-on-date="onDrop"
                @click-date="onClickDay"
                @click-event="onClickEvent"
            >
                <calendar-view-header
                    slot="header"
                    slot-scope="{ headerProps }"
                    :header-props="headerProps"
                    @input="setShowDate"
                />
            </calendar-view>
        </div>
  </div>
</template>

<script>

// Load CSS from the local repo
//require("/Users/natesnapp/working/natesnapp/vue-simple-calendar/static/css/default.css")
require("./calendar-theme.css")
//require("/Users/natesnapp/working/natesnapp/vue-simple-calendar/static/css/holidays-us.css")
import {
    CalendarView,
    CalendarViewHeader,
    CalendarMathMixin,
//} from "vue-simple-calendar" // published version
} from "/Users/natesnapp/working/natesnapp/vue-simple-calendar/src/components/bundle.js" // local repo

  import { formatDate } from '~/assets/dateUtils.js'

  export default {
    //title: 'Dragonflies Team Page',
    layout: 'soccer',
    description: 'The page for our favorite RAGE team',
    components: {
        CalendarView,
        CalendarViewHeader,
    },
    mixins: [CalendarMathMixin],
    data() {
      return {
            /* Show the current month, and give it some fake events to show */
            showDate: new Date(2021, 8, 1, 0, 0),
            message: "",
            startingDayOfWeek: 0,
            disablePast: false,
            disableFuture: false,
            displayPeriodUom: "month",
            displayPeriodCount: 1,
            showEventTimes: true,
            newEventTitle: "",
            newEventStartDate: "",
            newEventEndDate: "",
            useDefaultTheme: true,
            useHolidayTheme: true,
            useTodayIcons: false,
            events: [
                {
                    id: "p1",
                    startDate: "2021-07-30",
                    title: "<b>8-8:45am @ Temple Ridge</b><br />First team practice"
                },
                {
                    id: "p2",
                    startDate: "2021-08-03",
                    title: "<b>8-8:45am @ Temple Ridge</b><br />Practice"
                },
                {
                    id: "p3",
                    startDate: "2021-08-10",
                    title: "<b>8-8:45am @ Temple Ridge</b><br />Practice"
                },
                {
                    id: "p4",
                    startDate: "2021-08-16",
                    title: "<b>8-9am @ Temple Ridge</b><br />Practice"
                },
                {
                    id: "a1",
                    startDate: "2021-08-18",
                    title: "<b>6-7pm @ Harvey Park</b><br />Pizza party and vote on team name",
                    classes: "blue"
                },
                {
                    id: "g1",
                    startDate: "2021-08-21",
                    title: "<b>12:30pm vs Deerfield 208</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g2",
                    startDate: "2021-08-24",
                    title: "<b>6:45pm vs Deerfield 206</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g3",
                    startDate: "2021-08-28",
                    title: "<b>10:10am vs Deerfield 204</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g4",
                    startDate: "2021-09-01",
                    title: "<b>5:30pm vs Deerfield 202</b><br /><span style=\"background-color:#ff3333\">Red</span> jersey",
                    classes: "pink"
                },
                {
                    id: "a2",
                    startDate: "2021-09-04",
                    endDate: "2021-09-06",
                    title: "Labor Day weekend - No Soccer",
                    classes: "blue"
                },
                {
                    id: "a2a",
                    startDate: "2021-09-07",
                    endDate: "2021-09-10",
                    title: "No Practice - Coach Snapp in Alaska!",
                },
                {
                    id: "e1",
                    startDate: "2021-09-22",
                    title: "<b>5:30pm Pictures!</b><br />Practice @ Coach Snapp's backyard",
                    classes: "orange"
                },
                {
                    id: "g5",
                    startDate: "2021-09-16",
                    title: "<b>6:45pm vs Deerfield 205</b><br /><span style=\"background-color:#ff3333\">Red</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g6",
                    startDate: "2021-09-18",
                    title: "<b>10:10am vs Deerfield 210</b><br /><span style=\"background-color:#ff3333\">Red</span> jersey",
                    classes: "pink"
                },
                {
                    id: "p6",
                    startDate: "2021-09-29",
                    title: "<b>6pm @ Temple Ridge</b><br />Practice"
                },
                {
                    id: "g8",
                    startDate: "2021-10-02",
                    title: "<b>12:30pm vs Deerfield 209</b><br /><span style=\"background-color:#ff3333\">Red</span> jersey",
                    classes: "pink"
                },
                {
                    id: "a3",
                    startDate: "2021-10-06",
                    title: "<b>6-7pm @ Coach Snapp's house</b><br />End of season party and trophies",
                    classes: "blue"
                },
            ],
      }
    },
    computed: {
        userLocale() {
            return this.getDefaultBrowserLocale
        },
        dayNames() {
            return this.getFormattedWeekdayNames(this.userLocale, "long", 0)
        },
        themeClasses() {
            return {
                "theme-default": this.useDefaultTheme,
                "holiday-us-traditional": this.useHolidayTheme,
                "holiday-us-official": this.useHolidayTheme,
            }
        },
    },
    mounted() {
        this.newEventStartDate = this.isoYearMonthDay(this.today())
        this.newEventEndDate = this.isoYearMonthDay(this.today())
    },
    methods: {
      formatDate,
      displayArr(arr) {
        return arr.join(', ');
      },
        periodChanged(range, eventSource) {
            // Demo does nothing with this information, just including the method to demonstrate how
            // you can listen for changes to the displayed range and react to them (by loading events, etc.)
            console.log(eventSource)
            console.log(range)
        },
        thisMonth(d, h, m) {
            const t = new Date()
            return new Date(t.getFullYear(), t.getMonth(), d, h || 0, m || 0)
        },
        onClickDay(d) {
            this.message = `You clicked: ${d.toLocaleDateString()}`
        },
        onClickEvent(e) {
            this.message = `You clicked: ${e.title}`
        },
        setShowDate(d) {
            this.message = `Changing calendar view to ${d.toLocaleDateString()}`
            this.showDate = d
        },
        onDrop(event, date) {
            this.message = `You dropped ${event.id} on ${date.toLocaleDateString()}`
            // Determine the delta between the old start date and the date chosen,
            // and apply that delta to both the start and end date to move the event.
            const eLength = this.dayDiff(event.startDate, date)
            event.originalEvent.startDate = this.addDays(event.startDate, eLength)
            event.originalEvent.endDate = this.addDays(event.endDate, eLength)
        },
        clickTestAddEvent() {
            this.events.push({
                startDate: this.newEventStartDate,
                endDate: this.newEventEndDate,
                title: this.newEventTitle,
                id:
                    "e" +
                    Math.random()
                        .toString(36)
                        .substr(2, 10),
            })
            this.message = "You added an event!"
        },
    }
  };

</script>

<style lang="less" scoped>
  @import "../../assets/variables.less";

  .cv-week {
    flex-basis: 6em;
  }

  a {
    border-bottom: 0;
  }

  .page-preview {
    &:first-child {
      margin-top: 1em;
    }
    margin-bottom: 3.5em;

    header {
      h2 {
        font-size: 40px;
      }
    }

    footer {
      display: flex;
      color: @gray-light;
      font-size: .9em;
      font-family: @font-family-sans-serif2;
      font-weight: 300;
      p {
        margin-left: auto;
        padding-left: 20px;
        text-align: right;
        text-indent: 0;
        white-space: nowrap;
      }
    }

    .header-info {
      display: flex;
      justify-content: space-evenly;
      font-size: 1.2em;
      & > div {
        flex: 1 1 auto;
      }
      .date {
        /*padding-left: 20px;*/
        white-space: nowrap;
      }
      .tags {
        padding-left: 20px;
        justify-self: right;
      }
    }
  }

  html,
  body {
      height: 100%;
      margin: 0;
      background-color: #f7fcff;
  }
  p {
      text-indent: 0 !important;
  }
  #app {
      display: flex;
      flex-direction: row;
      font-family: Calibri, sans-serif;
      width: 95vw;
      min-width: 30rem;
      max-width: 100rem;
      min-height: 40rem;
      margin-left: auto;
      margin-right: auto;
  }
  .calendar-controls {
      margin-right: 1rem;
      min-width: 14rem;
      max-width: 14rem;
  }
  .calendar-parent {
      display: flex;
      flex-direction: column;
      flex-grow: 1;
      overflow-x: hidden;
      overflow-y: hidden;
      max-height: 100vh;
      background-color: white;
  }
  /* For long calendars, ensure each week gets sufficient height. The body of the calendar will scroll if needed */
  .cv-wrapper.period-month.periodCount-2 .cv-week,
  .cv-wrapper.period-month.periodCount-3 .cv-week,
  .cv-wrapper.period-year .cv-week {
      min-height: 8rem;
  }
  /* These styles are optional, to illustrate the flexbility of styling the calendar purely with CSS. */
  /* Add some styling for events tagged with the "birthday" class */
  .theme-default .cv-event.birthday {
      background-color: #e0f0e0;
      border-color: #d7e7d7;
  }
  .theme-default .cv-event.birthday::before {
      content: "\1F382"; /* Birthday cake */
      margin-right: 0.5em;
  }

</style>
