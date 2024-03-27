<template>
    <div>
        <h1 class="title">BMI 계산기</h1>
        <form @submit.prevent="calculateBMI">
            <label for="height">키 (cm):</label>
            <input type="number" id="height" v-model.number="height" required>
            <label for="weight">몸무게 (kg):</label>
            <input type="number" id="weight" v-model.number="weight" required>
            <button type="submit">BMI 계산하기</button>
        </form>
        <div v-if="bmi !== null">
            <h2>BMI:</h2>
            <p @click="showImage('저체중')">{{ bmi.toFixed(2) }}</p>
            <p @click="showImage('정상체중')">{{ BMICategory(bmi) }}</p>
            <p @click="showImage('과체중')">{{ BMICategory(bmi) }}</p>
            <p @click="showImage('비만')">{{ BMICategory(bmi) }}</p>
        </div>
        <div v-if="selectedImage !== ''">
            <img class="bmi--img" :src="selectedImage">
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
            selectedImage: ''
        };
    },
    methods: {
        calculateBMI() {
            const heightMeter = this.height / 100;
            this.bmi = this.weight / (heightMeter * heightMeter);
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
        showImage(category) {
            if (category === '저체중') {
                this.selectedImage = '/Users/iminji/vueProject/src/assets/low.png';
            } else if (category === '정상체중') {
                this.selectedImage = '/Users/iminji/vueProject/src/assets/normal.jpeg';
            } else if (category === '과체중') {
                this.selectedImage = '/Users/iminji/vueProject/src/assets/high.jpeg';
            } else {
                this.selectedImage = '/Users/iminji/vueProject/src/assets/danger.jpeg';
            }
        }
    }
};
</script>

<style>
.title {
    color: aqua;
}
.bmi--img {
    width: 150px;
}
</style>
