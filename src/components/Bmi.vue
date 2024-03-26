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
        <!-- toFixed(숫자)는 소수점 둘쨰 자리까지 반올림 할 수 있는 기능(bmi로 도출된 결과값을)-->
        <p>{{ BMICategory(bmi) }}</p>
    </div>
    </div>
</template>
<style>
.title {
    color: aqua;
}
/* .greeting으로 글씨색이 변하지 않아 클래스를 부여한 후 색을 변환함 */
</style>
<script>
export default {
    data() {
    return {
        height: null,
        weight: null,
        bmi: null
    };
    //초기값을 null로 설정
    },
    methods: {
    calculateBMI() {
        const heightMeter = this.height / 100;
        //입력된 키를 미터로 변환해주는 공식
        //data()로 정의된 데이터는 this로 가리킬 수 있음
        this.bmi = this.weight / (heightMeter * heightMeter);
        //몸무게 / 미터로바뀐키 * 미터로바뀐키
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

