<template>
  <div>
    <img src="./imgs/dragonflys.png" />
    <h2>Week 1</h2>
    <p>
    Welcome to the team! This is going to be a fun season and lots to look forward to. My name is Nate Snapp and I am a first year soccer coach. My athletic background includes hockey, cross country, and yes, soccer! My occupation is in cybersecurity as an engineer working down in Santa Clara.
    </p>
    <p>
    This site is intended to gather a list of important announcements, provide a calendar of events, and hopefully even showcase our wonderful young players.
    </p>
        <div class="calendar-parent">
            <calendar-view
                :events="events"
                :show-date="showDate"
                :time-format-options="{hour: 'numeric', minute:'2-digit'}"
                :enable-drag-drop="true"
                eventContentHeight="3.5em"
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
            showDate: new Date(2019, 7, 1, 0, 0),
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
                    startDate: "2019-08-02",
                    title: "<b>6pm @ Muirwood</b><br />First team meet-and-greet"
                },
                {
                    id: "p2",
                    startDate: "2019-08-09",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice"
                },
                {
                    id: "p3",
                    startDate: "2019-08-14",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice"
                },
                {
                    id: "a1",
                    startDate: "2019-08-16",
                    endDate: "2019-08-18",
                    title: "Coach Snapp out of town",
                    classes: "blue"
                },
                {
                    id: "p4",
                    startDate: "2019-08-23",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice"
                },
                {
                    id: "p5",
                    startDate: "2019-08-28",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice"
                },
                {
                    id: "a2",
                    startDate: "2019-08-30",
                    title: "Rest Up for Parade!",
                    classes: "blue"
                },
                {
                    id: "e1",
                    startDate: "2019-08-31",
                    title: "<b>7:00am @ Main Street</b><br />Opening Parade",
                    classes: "orange"
                },
                {
                    id: "e2",
                    startDate: "2019-09-14",
                    title: "<b>Picture Day!</b><br />Details to come",
                    classes: "orange"
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
      max-height: 80vh;
      background-color: white;
  }
  /* For long calendars, ensure each week gets sufficient height. The body of the calendar will scroll if needed */
  .cv-wrapper.period-month.periodCount-2 .cv-week,
  .cv-wrapper.period-month.periodCount-3 .cv-week,
  .cv-wrapper.period-year .cv-week {
      min-height: 6rem;
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
