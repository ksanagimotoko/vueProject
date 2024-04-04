<template>
    <div class="container-fluid" :style="{ backgroundColor: bgColor, height: '1000px' }">
        <label for="ColorInput" class="form-label">배경색을 고르세요</label>
        <input type="color" class="form-control form-control-color" id="ColorInput" value="#E5D3FD" @input="changeBgColor">
        <label for="textColorInput" class="form-label">글씨색을 고르세요</label>
        <input type="color" class="form-control form-control-color" id="textColorInput" value="#000000" @input="changeTxColor">

        <div class="row justify-content-center mt-4">
            <div class="col-md-8">
                <h2 class="text-center" :style="{ color: textColor }">일정 추가</h2>
                <div class="calendar">
                    <div class="calendar-header">
                        <button @click="prevMonth">&lt;</button>
                        <h3>{{ currentMonth }}</h3>
                        <button @click="nextMonth">&gt;</button>
                    </div>
                    <div class="calendar-body">
                        <div class="week" v-for="(week, index) in calendar" :key="index">
                            <div v-for="(day, index) in week" :key="index" class="day" :class="{ today: isToday(day), selected: isSelected(day) }" @dblclick="openEventModal(day)">
                                {{ day.date }}
                                <div class="events">
                                    <div v-for="event in day.events" :key="event.id" class="event">
                                        {{ event.title }}
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 일정 입력 모달 -->
    <div class="modal" id="eventModal" tabindex="-1" role="dialog" ref="eventModal">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <form @submit.prevent="saveEvent">
                    <div class="modal-header">
                        <h5 class="modal-title">일정 추가</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="closeEventModal">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <input type="text" v-model="newEvent.title" class="form-control" placeholder="최대 10자 입력 가능">
                    </div>
                    <!-- 일정 보기 -->
                    <div class="modal-body">
                        <ul>
                            <li v-for="event in newEvent.events" :key="event.id">{{ event.title }}</li>
                        </ul>
                    </div>
                    <div class="modal-footer">
                        <button type="submit" class="btn btn-primary">저장</button>
                        <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="closeEventModal">취소</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

</template>

<script>
export default {
    data() {
        return {
            bgColor: '#E5D3FD',
            textColor: '#000000',
            selectedDate: '',
            events: [],
            currentDate: new Date(),
            currentMonth: '',
            calendar: [],
            newEvent: {
                title: '',
                events: [] // 일정 보관
            }
        };
    },
    computed: {
        currentDateFormatted() {
            return `${this.currentDate.getFullYear()}-${(this.currentDate.getMonth() + 1).toString().padStart(2, '0')}-${this.currentDate.getDate().toString().padStart(2, '0')}`;
        },
    },
    methods: {
        changeBgColor(event) {
            this.bgColor = event.target.value;
        },
        changeTxColor(event) {
            this.textColor = event.target.value;
        },
        isToday(day) {
            const today = new Date();
            return day.date === today.getDate() && this.currentDate.getMonth() === today.getMonth() && this.currentDate.getFullYear() === today.getFullYear();
        },
        isSelected(day) {
            return this.selectedDate === day.date;
        },
        openEventModal(day) {
            this.selectedDate = day.date;
            // 일정 가져오기
            this.newEvent.events = this.getEventsForDate(day.date);
            this.$refs.eventModal.classList.add('show');
            this.$refs.eventModal.style.display = 'block';
            document.body.classList.add('modal-open');
        },
        closeEventModal() {
            this.selectedDate = '';
            this.newEvent.title = ''; // 리셋
            this.newEvent.events = []; // 일정 초기화
            this.$refs.eventModal.classList.remove('show');
            this.$refs.eventModal.style.display = 'none';
            document.body.classList.remove('modal-open');
        },
        saveEvent() {
            if (this.newEvent.title.trim() !== '') {
                if (this.newEvent.title.length > 10) {
                    this.newEvent.title = this.newEvent.title.substring(0, 10);
                }
                const event = {
                    title: this.newEvent.title,
                    date: this.selectedDate
                };
                this.events.push(event); // 일정 추가
                this.updateCalendar(); // 캘린더 업데이트
                this.newEvent.title = ''; // 리셋
                this.newEvent.events = this.getEventsForDate(this.selectedDate); // 일정 초기화
            }
        },
        prevMonth() {
            this.currentDate.setMonth(this.currentDate.getMonth() - 1);
            this.updateCalendar();
        },
        nextMonth() {
            this.currentDate.setMonth(this.currentDate.getMonth() + 1);
            this.updateCalendar();
        },
        updateCalendar() {
            const year = this.currentDate.getFullYear();
            const month = this.currentDate.getMonth();
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            this.currentMonth = `${year}년 ${month + 1}월`;

            const calendar = [];
            let week = [];
            let dayOfWeek = firstDay.getDay();

            for (let i = 0; i < dayOfWeek; i++) {
                week.push({ date: '' });
            }

            for (let day = 1; day <= lastDay.getDate(); day++) {
                const formattedDate = `${year}-${(month + 1).toString().padStart(2, '0')}-${day.toString().padStart(2, '0')}`;
                const eventsForDate = this.getEventsForDate(formattedDate);
                week.push({ date: day, events: eventsForDate });
                if (week.length === 7) {
                    calendar.push(week);
                    week = [];
                }
            }

            if (week.length > 0) {
                while (week.length < 7) {
                    week.push({ date: '' });
                }
                calendar.push(week);
            }

            this.calendar = calendar;
        },
        getEventsForDate(formattedDate) {
            return this.events.filter(event => event.date === formattedDate);
        },
    },
    mounted() {
        this.updateCalendar();
    },
};
</script>

<style>
.calendar {
    border: 1px solid #ccc;
    border-radius: 5px;
    overflow: hidden;
    margin-top: 20px;
}

.calendar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background-color: #f0f0f0;
}

.calendar-body {
    margin-top: 10px;
}

.week {
    display: flex;
    flex-wrap: wrap;
}

.day {
    flex-basis: calc(100% / 7);
    padding: 10px;
    text-align: center;
    border: 1px solid #ccc;
    cursor: pointer;
}

.day.today {
    background-color: #e0e0e0;
}

.day.selected {
    background-color: #c5cae9;
}

.events {
    margin-top: 5px;
}

.event {
    padding: 3px;
    background-color: #f7f7f7;
    border-radius: 3px;
    font-size: 0.8em;
}

/* Modal Styles */
.modal {
    display: none;
    position: fixed;
    z-index: 1050;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    overflow: hidden;
    outline: 0;
}

.modal-dialog {
    position: relative;
    width: auto;
    margin: 10px;
}

.modal-content {
    position: relative;
    background-color: #fff;
    border: 1px solid rgba(0, 0, 0, 0.2);
    border-radius: 0.3rem;
    outline: 0;
}

.modal-header {
    padding: 15px;
    border-bottom: 1px solid #e9ecef;
}

.modal-body {
    position: relative;
    padding: 15px;
}

.modal-footer {
    padding: 15px;
    text-align: right;
    border-top: 1px solid #e9ecef;
}
</style>
