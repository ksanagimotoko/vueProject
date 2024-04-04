<template>
    <div class="wrap">
        <div ref="calendar" class="calendar"></div>
        <div style="clear:both"></div>
    </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue' // FullCalendar Vue.js 버전 임포트
import dayGridPlugin from '@fullcalendar/daygrid' // FullCalendar의 DayGrid 플러그인 임포트
import interactionPlugin from '@fullcalendar/interaction' // FullCalendar의 interaction 플러그인 임포트

export default {
    name: 'CalendarComponent',
    components: {
        FullCalendar // FullCalendar를 Vue 컴포넌트로 등록
    },
    mounted() {
        let date = new Date();
        let d = date.getDate();
        let m = date.getMonth();
        let y = date.getFullYear();

        // FullCalendar 초기화
        let calendar = new FullCalendar(this.$refs.calendar, {
            plugins: [dayGridPlugin, interactionPlugin], // 사용할 플러그인 등록
            headerToolbar: {
                left: 'prev,next today',
                center: 'title',
                right: 'dayGridMonth,dayGridWeek,dayGridDay'
            },
            editable: true,
            firstDay: 1,
            selectable: true,
            initialView: 'dayGridMonth',
            events: [
                {
                    title: '하루 종일 이벤트',
                    start: new Date(y, m, 1)
                },
                // 나머지 이벤트들도 이와 같은 형식으로 추가
            ],
            select: this.handleDateSelect // 날짜 선택 시 이벤트 핸들러 등록
        });
    },
    methods: {
        handleDateSelect(info) {
            let title = prompt('이벤트 제목:');
            if (title) {
                this.$refs.calendar.addEvent({
                    title: title,
                    start: info.startStr,
                    end: info.endStr,
                    allDay: info.allDay
                });
            }
        }
    }
}
</script>

<style scoped>
    .wrap {
        width: 1100px;
        margin: 0 auto;
    }

    .body {
        margin-top: 40px;
        text-align: center;
        font-size: 14px;
        font-family: "Helvetica Nueue",Arial,Verdana,sans-serif;
        background-color: #DDDDDD;
    }

    .external-events {
        float: left;
        width: 150px;
        padding: 0 10px;
        text-align: left;
    }

    .external-events h4 {
        font-size: 16px;
        margin-top: 0;
        padding-top: 1em;
    }

    .external-event { /* 실제 이벤트 모양을 모방하기 위해 시도 */
        margin: 10px 0;
        padding: 2px 4px;
        background: #3366CC;
        color: #fff;
        font-size: .85em;
        cursor: pointer;
    }

    .external-events p {
        margin: 1.5em 0;
        font-size: 11px;
        color: #666;
    }

    .external-events p input {
        margin: 0;
        vertical-align: middle;
    }

    .calendar {
        margin: 0 auto;
        width: 900px;
        background-color: #FFFFFF;
        border-radius: 6px;
        box-shadow: 0 1px 2px #C3C3C3;
    }
</style>
