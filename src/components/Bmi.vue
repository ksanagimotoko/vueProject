<template>
    <div>
        <h1 class="title">BMI 계산기</h1>
        <form @submit.prevent="calculateBMI">
            <label for="height">키 (cm):</label>
            <input type="number" id="height" v-model.number="height" required>
            <!-- input태그 사용 할 때 required를 같이 써주면 빈칸으로 결과값을 눌렀을 때 팝업이 나타나게 할 수 있음 -->
            <label for="weight">몸무게 (kg):</label>
            <input type="number" id="weight" v-model.number="weight" required>
            <button type="submit">BMI 계산하기</button>
        </form>
        <div v-if="bmi !== null">
            <!--v-if는 조건이 참일 때만 결과값을 보여줌-->
            <h2>BMI:</h2>
            <p>{{ bmi.toFixed(2) }}</p>
            <!-- toFixed(숫자)는 소수점 둘째 자리까지 반올림 할 수 있는 기능(bmi로 도출된 결과값을)-->
            <p>{{ BMICategory(bmi) }}</p>
            <img class="bmi--img" v-if="selectImg === '저체중'" src='/Users/iminji/vueProject/src/assets/low.png'>
            <img class="bmi--img" v-else-if="selectImg === '정상체중'" src='/Users/iminji/vueProject/src/assets/normal.jpeg'>
            <img class="bmi--img" v-else-if="selectImg === '과체중'" src='/Users/iminji/vueProject/src/assets/high.jpeg'>
            <img class="bmi--img" v-else src='/Users/iminji/vueProject/src/assets/danger.jpeg'>
            <!-- https://goodmemory.tistory.com/149 이 사이트 도움으로 이미지 설정 -->
        </div>
    </div>
</template>

<style>
.title {
    color: aqua;
}
.bmi--img {
    width: 150px;
}
</style>

<script>
export default {
    data() {
        return {
            height: null,
            weight: null,
            bmi: null,
            selectImg: ''
        };
    },
        methods: {
        calculateBMI() {
            const heightMeter = this.height / 100;
            this.bmi = this.weight / (heightMeter * heightMeter);
            this.selectImg = this.BMICategory(this.bmi);
        },
        BMICategory(bmi) {
            if (bmi < 18.5) {
                return "저체중";
            } else if (bmi < 25) {
                return "정상체중";
            } else if (bmi < 30) {
                return "과체중";
            } else {
                return "비만";
            }
        }
    }
};
</script>
