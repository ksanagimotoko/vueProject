<template>
    <div class="container-fluid" :style="{ backgroundColor: bgColor, height: '600px' }">
    <label for="exampleColorInput" class="form-label"> 배경색을 고르세요 </label>
      <input type="color" class="form-control form-control-color" id="exampleColorInput" value="#E5D3FD" title="Choose your color" @input="changeBgColor">
      <div class="row justify-content-center">
        <div class="col-md-6">
          <h1 class="text-center">BMI 계산기</h1>
          <form @submit.prevent="calculateBMI">
            <div class="form-group">
              <label for="height">키 (cm):</label>
              <input type="number" id="height" v-model.number="height" required class="form-control" placeholder="160">
            </div>
            <div class="form-group">
              <label for="weight">몸무게 (kg):</label>
              <input type="number" id="weight" v-model.number="weight" required class="form-control" placeholder="50">
            </div>
            <button type="submit" class="btn btn-primary">BMI 계산하기</button>
          </form>
        </div>
        <div class="col-md-6 result" v-if="bmi !== null">
          <h2>BMI:</h2>
          <p>{{ bmi.toFixed(2) }}</p>
          <p>{{ BMICategory(bmi) }}</p>
          <img class="bmi--img" v-if="selectImg === '/Users/iminji/vueProject/src/assets/low.jpeg'" src='/Users/iminji/vueProject/src/assets/low.jpeg'>
        <img class="bmi--img" v-else-if="selectImg === '/Users/iminji/vueProject/src/assets/normal.jpeg'" src='/Users/iminji/vueProject/src/assets/normal.jpeg'>
        <img class="bmi--img" v-else-if="selectImg === '/Users/iminji/vueProject/src/assets/high.jpeg'" src='/Users/iminji/vueProject/src/assets/high.jpeg'>
        <img class="bmi--img" v-else-if="selectImg === '/Users/iminji/vueProject/src/assets/danger.jpeg'" src='/Users/iminji/vueProject/src/assets/danger.jpeg'>
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
        bgColor: '#E5D3FD' // 초기 배경색
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
          return '/Users/iminji/vueProject/src/assets/low.jpeg';
        } else if (this.bmi < 25) {
          return '/Users/iminji/vueProject/src/assets/normal.jpeg';
        } else if (this.bmi < 30) {
          return '/Users/iminji/vueProject/src/assets/high.jpeg';
        } else {
          return '/Users/iminji/vueProject/src/assets/danger.jpeg';
        }
      },
      changeBgColor(event) {
        this.bgColor = event.target.value;
      }
    }
  };
  </script>
  