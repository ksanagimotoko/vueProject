<template>
  <div id="app">
    <div class="container">
      <h2> BMI 계산기</h2>
      <div>
        <label for = "height"> 키(cm) : </label>
        <input type="number" id="height" v-model="height">
      </div>
      <div>
        <label for="weight"> 몸무게(kg) : </label>
        <input type="number" id="weight" v-model="weight">
  </div>

  <button @click="calculateBMI"> BMI 계산하기 </button>
  <button @click="reset"> 초기화 </button>
  <div class="result" v-if="bmi !== null">
    <h3> 당신의 BMI는 {{ bmi }} 입니다.</h3>
    <P> {{ bmiCategory }} </P>
    <img :src="bmiImage" alt="BMI Image">
  </div>
</div>
  </div>

</template>


<script>

import underweightImage from '@/assets/bmiImages/under.png';
import normalImage from '@/assets/bmiImages/normal.png';
import overweightImage from '@/assets/bmiImages/over.png';
import obese1Image from '@/assets/bmiImages/ob1.png';
import obese2Image from '@/assets/bmiImages/ob2.png';
import obese3Image from '@/assets/bmiImages/ob3.png';

export default {
  data() {
    return {
      height: null,
      weight: null,
      bmi: null,
      bmiImages: {
        underweight: underweightImage,
        normal: normalImage,
        overweight: overweightImage,
        obese1: obese1Image,
        obese2: obese2Image,
        obese3: obese3Image

      }
    };
  },
  computed: {
    bmiCategory() {
      if (this.bmi === null) return '';
      if (this.bmi < 18.5) return '저체중';
      else if (this.bmi < 24.9) return '정상';
      else if (this.bmi < 29.9) return '과체중';
      else return '비만';
    },
    bmiImage() {
      if (this.bmi === null) return '';
      if (this.bmi < 18.5) return this.bmiImages.underweight;
      else if (this.bmi < 24.9) return this.bmiImages.normal;
      else if (this.bmi < 29.9) return this.bmiImages.overweight;
      else if (this.bmi < 34.9) return this.bmiImages.obese1;
      else if (this.bmi < 39.9) return this.bmiImages.obese2;
      else return this.bmiImages.obese3;
    }
  },
  methods: {
    calculateBMI() {
      if (this.height && this.weight) {
        const heightMeter = this.height / 100;
        this.bmi = (this.weight / (heightMeter * heightMeter)).toFixed(2);
      } else {
        alert('키와 몸무게를 입력해주세요.');
      }
    },
    reset() {
      this.height = null;
      this.weight = null,
      this.bmi = null;
    }
  }
};
</script>