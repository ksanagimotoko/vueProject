<template>
    <div class="container-fluid" :style="{ backgroundColor: bgColor, height: '1000vh' }">
        <label for="exampleColorInput" class="form-label"> 배경색을 고르세요 </label>
        <input type="color" class="form-control form-control-color" id="ColorInput" value="#E5D3FD" title="Choose your color" @input="changeBgColor">
        <label for="textColorInput" class="form-label"> 글씨색을 고르세요 </label>
        <input type="color" class="form-control form-control-color" id="textColorInput" value="ffffff" title="Choose your text color" @input="changeTxColor">
    
        <div class="row justify-content-center">
            <div class="col-md-6">
                <h1 class="text-center mt-3" :style="{ color: textColor }">BMI 계산기</h1>
                <form @submit.prevent="calculateBMI">
                    <div class="form-group mt-3">
                        <label for="height">키 (cm):</label>
                        <input type="number" id="height" v-model.number="height" required class="form-control" placeholder="160">
                    </div>
                    <div class="form-group ">
                        <label for="weight">몸무게 (kg):</label>
                        <input type="number" id="weight" v-model.number="weight" required class="form-control" placeholder="50">
                    </div>
                    <button type="submit" class="btn btn-primary mt-3">BMI 계산하기</button>
                </form>
            </div>
    
            <div class="col-md-6 result text-center mt-3" v-if="bmi !== null">
                <h2>BMI:</h2>
                <p>{{ bmi.toFixed(2) }}</p>
                <p>{{ BMICategory(bmi) }}</p>
                <img class="bmi--img" v-if="selectImg === '../assets/low.jpeg'" src='../assets/low.jpeg'>
                <img class="bmi--img" v-else-if="selectImg === '../assets/normal.jpeg'" src='../assets/normal.jpeg'>
                <img class="bmi--img" v-else-if="selectImg === '../assets/high.jpeg'" src='../assets/high.jpeg'>
                <img class="bmi--img" v-else-if="selectImg === '../assets/danger.jpeg'" src='../assets/danger.jpeg'>
            </div>
    
            <!-- 계산기 -->
            <div class="col-md-6 mt-5 text-center">
                <h2>계산기</h2>
            </div>
            <!-- 계산기 입력 필드 및 버튼 추가 -->
                <div>
                    <input type="text" v-model="calculation" class="form-control" placeholder="계산식을 입력하세요">
                    <button @click="calculate" class="btn btn-primary mt-3 text center">계산하기</button>
                    <p class="mt-3">결과: {{ result }}</p>
                </div>
            <!-- 사칙연산 필드 추가 -->
            <div class="col-md-6 text-center">
                <h2>사칙연산</h2>
            </div>
            <div class="inbtn">
                <div class="mt-3"><span class="badge bg-warning">a = </span> <input type="text" v-model="a"></div>
                <div class="mt-3"><span class="badge bg-warning">b = </span> <input type="text" v-model="b"></div>
            </div>
            <div class="btnn">
                <button type="submit" class="btn btn-outline-dark mt-3" @click="onClickPlus">덧셈</button>
                <button type="submit" class="btn btn-outline-success mt-3" @click="onClickMinus">뺄셈</button>
                <button type="submit" class="btn btn-outline-danger mt-3" @click="onClickMultiple">곱셈</button>
                <button type="submit" class="btn btn-outline-info mt-3" @click="onClickDivide">나눗셈</button>
                <button type="submit" class="btn btn-outline-primary mt-3" @click="onClickOther">퍼센트</button>
                <p>결과: {{ arithmeticResult }}</p>
            </div>
                
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            height: null,
            weight: null,
            bmi: null,
            selectImg: '',
            bgColor: '#E5D3FD',
            textColor: '#000000',
            calculation: '',
            result: null,
            a: '',
            b: '',
            arithmeticResult: null
        };
    },
    methods: {
        calculateBMI() {
            const heightMeter = this.height / 100;
            this.bmi = this.weight / (heightMeter * heightMeter);
            this.selectImg = this.getImage();
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
        },
        getImage() {
            if (this.bmi < 18.5) {
            return '../assets/low.jpeg';
            } else if (this.bmi < 25) {
            return '../assets/normal.jpeg';
            } else if (this.bmi < 30) {
            return '../assets/high.jpeg';
            } else {
            return '../assets/danger.jpeg';
            }
        },
        changeBgColor(event) {
            this.bgColor = event.target.value;
        },
        changeTxColor(event) {
            this.textColor = event.target.value;
        },
        calculate() {
            try {
                this.result = eval(this.calculation);
            } catch (error) {
                this.result = '잘못된 식입니다.';
            }
        },
        onClickPlus() {
            let k = this.a;
            let m = this.b;
            this.arithmeticResult = parseInt(this.a) + parseInt(this.b);
        },
        onClickMinus() {
            this.arithmeticResult = parseInt(this.a) - parseInt(this.b);
        },
        onClickMultiple() {
            this.arithmeticResult = parseInt(this.a) * parseInt(this.b);
        },
        onClickDivide() {
            this.arithmeticResult = parseInt(this.a) / parseInt(this.b);
        },
        onClickOther() {
            this.arithmeticResult = parseInt(this.a) % parseInt(this.b);
        }
    }
};
</script>
<style>
.inbtn {
    display: inline-block;
}
.btnn{
    display :inline-block;
}

</style>