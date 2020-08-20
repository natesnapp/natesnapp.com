<template>
  <div>
    <!--<img src="./imgs/dragonflies.jpg" />-->
    <h2>Week 6</h2>
    <p>I hope all have had a wonderful Labor Day weekend. I'd like to recap week 4 and the official open of the soccer season. After a great practice and pizza party, it was great to see everyone at the opening parade! All the girls looked great in their costumes and did really well in their first game.</p>
    <p>Since this is the first game of the season, I am still working some things out. A few points:</p>
    <ul>
        <li>We'll start warming up 15 minutes before game time. So if the game is 3:30 pm, we'll start kicking the ball around behind the field at 3:15pm. I'll bring my equipment and try to have the team banner set up so you can find us easily.</li>
        <li>I have been rotating the girls quickly... almost like a hockey line-up 😆. A lot of this is to keep the girls in touch with the game, as well as the girls tiring quickly. This will probably continue for another game or two as we build their endurance. Ultimately, I would like to be able to keep girls in for about 3 minutes at a time, and I think we'll get there with more practice. I've already seen a difference just from our first few weeks!</li>
        <li>Thank you for all your help to keep the girls focused on the play time. I know it is super fun for them to be seen and supported by family and friends. No problem if they decide they want to come off because they are tired. Last year Izzy would do summersaults or even run backwards when she got bored! They are young and learning. If there is anything I can do to make the experience better for your girl, please let me know! Let them know the team is excited to have them, and if they want to come give you five or hugs during the game, just let them know the game is on and to keep going!</li>
        <li>Also thanks for helping with the rule that players and coach be on one side and parents/fans on the other of the field. We have new players and I know it is hard. Feel free to run over or stand in the wings if you think it will help best encourage your player. I'll also do my best to encourage the other teams to follow the same rule, but I understand that sometimes it can be tough to find shade.</li>
        </ul>
    <p>I am looking to see if we should adjust the day for practice, as I may have a commitment for my oldest daughter who is starting up field hockey which is Friday at 6:30pm. For this week, let's just shift the practice time back to 5pm if that works. Let me know if you have any concern if we do practice on Wed or Thursday, as I know we need to have a consistent day and time. Thanks for your support!</p>
    <p>See everyone for practice and the game this week!</p>
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
                    title: "<b>5:30pm @ Muirwood</b><br />First team practice"
                },
                {
                    id: "p2",
                    startDate: "2019-08-09",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice"
                },
                {
                    id: "p3",
                    startDate: "2019-08-14",
                    title: "Practice <b>cancelled</b> due to heat!!"
                },
                {
                    id: "p3a",
                    startDate: "2019-08-15",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice and pick up uniforms/parade wings"
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
                    startDate: "2019-08-22",
                    title: "<b>5:30pm @ Muirwood</b><br />Practice, Party at 7600 Olive Drive!"
                },
                {
                    id: "a2",
                    startDate: "2019-08-23",
                    title: "Rest Up for Parade!",
                    classes: "blue"
                },
                {
                    id: "e1",
                    startDate: "2019-08-24",
                    title: "<b>7:00am @ Main Street</b><br />Opening Parade",
                    classes: "orange"
                },
                {
                    id: "g1",
                    startDate: "2019-08-24",
                    title: "<b>10am vs Dalmations</b><br /><span style=\"background-color:#ff9933\">Orange jersey</span>",
                    classes: "pink"
                },
                {
                    id: "a3",
                    startDate: "2019-08-30",
                    endDate: "2019-09-02",
                    title: "Labor Day weekend - No Practice",
                    classes: "blue"
                },
                {
                    id: "p4",
                    startDate: "2019-09-06",
                    title: "<b>5:00pm</b> @ Muirwood<br />Practice"
                },
                {
                    id: "g2",
                    startDate: "2019-09-07",
                    title: "<b>3:30pm vs Dashers</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "p5",
                    startDate: "2019-09-13",
                    title: "<b>5:00pm</b> @ Muirwood<br />Practice"
                },
                {
                    id: "e2",
                    startDate: "2019-09-14",
                    title: "<b>Picture Day!</b><br />Details to come",
                    classes: "orange"
                },
                {
                    id: "g3",
                    startDate: "2019-09-14",
                    title: "<b>8:00am vs Dandelions</b><br /><span style=\"background-color:#ff9933\">Orange</span> jersey",
                    classes: "pink"
                },
                {
                    id: "p6",
                    startDate: "2019-09-20",
                    title: "<b>5:00pm</b> @ Muirwood<br />Practice"
                },
                {
                    id: "g4",
                    startDate: "2019-09-21",
                    title: "<b>9:15am vs Dancers</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "p6",
                    startDate: "2019-09-27",
                    title: "<b>5:00pm</b> @ Muirwood<br />Practice"
                },
                {
                    id: "g5",
                    startDate: "2019-09-28",
                    title: "<b>11:45am vs Dazzlers</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "p7",
                    startDate: "2019-10-04",
                    title: "<b>5:00pm</b> @ Muirwood<br />Practice"
                },
                {
                    id: "g6",
                    startDate: "2019-10-05",
                    title: "<b>3:30pm vs Diamonds</b><br /><span style=\"background-color:#ff9933\">Orange</span> jersey",
                    classes: "pink"
                },
                {
                    id: "p8",
                    startDate: "2019-10-11",
                    title: "<b>5:00pm</b> @ Muirwood<br />Practice"
                },
                {
                    id: "g7",
                    startDate: "2019-10-12",
                    title: "<b>2:15pm vs Doves</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g8",
                    startDate: "2019-10-19",
                    title: "<b>2:15pm vs Dolphins</b><br /><span style=\"background-color:#ff9933\">Orange</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g9",
                    startDate: "2019-10-26",
                    title: "<b>1:00pm vs Daffodils</b><br /><span style=\"background-color:#ff9933\">Orange</span> jersey",
                    classes: "pink"
                },
                {
                    id: "g7",
                    startDate: "2019-11-02",
                    title: "<b>11:45pm vs Doodlebugs</b><br /><span style=\"background-color:#999999\">Grey</span> jersey",
                    classes: "pink"
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
