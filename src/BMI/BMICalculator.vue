<template>
  <div id="app">
    <div class="container">

      <div class="row mt-3 tip">
        <div class="col-md-12 d-flex justify-content-end">
            <button @click="tiptool" class="btn btn-secondary btn-block "> 팁 보기 </button>
          </div>
      </div>

      <div class="row justify-content-center">
        <div class="col-md-6">

          <h2 class="title mt-5 mb-4 text-center"> BMI 계산기</h2>

          <div class="form-group">
            <label for = "height"> 키(cm) : </label>
            <input type="number" class="form-control" id="height" v-model="height">
          </div>

          <div class="form-group">
            <label for="weight"> 몸무게(kg) : </label>
            <input type="number" class="form-control" id="weight" v-model="weight">
          </div>

          <button @click="calculateBMI" class="btn btn-primary btn-block"> BMI 계산하기 </button>
          <button @click="reset" class="btn btn-primary btn-block"> 초기화 </button>

        </div>

    <div class="result row justify-content-center mt-4" v-if="bmi !== null">
      <div class="col-md-6">
          <div class="card">
            <div class="card-body">
              <h4> 당신의 BMI는 {{ bmi }} 입니다.</h4>
              <P> {{ bmiCategory }} </P>
              <img :src="bmiImage" alt="BMI Image" class="bmi-image">
            </div>
          </div>
        </div>
      </div>

      <div v-if="showTip" class="tip card">
              <div class="card-body">
                <h4>{{ showTipTool.title }}</h4>
                <p>{{ showTipTool.description }}</p>
              </div>
            </div>
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
      showTip: false,
      tips: [
        { title: 'Tip 1', description: '하루 세번 규칙적인 식사를 해야 한다.' },
        { title: 'Tip 2', description: '과일과 야채를 많이 먹는다.' },
        { title: 'Tip 3', description: '고단백 식단을 구성한다.' },
        { title: 'Tip 4', description: '백색 식품을 머리해야 한다.' },
        { title: 'Tip 5', description: '음료수 섭취를 줄인다.' }
      ],
      showTipToolIndex: 0,
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
      else if (this.bmi < 34.9) return '경도비만';
      else if (this.bmi < 39.9) return '중도비만';
      else return '과도비만';
    },
    bmiImage() {
      if (this.bmi === null) return '';
      if (this.bmi < 18.5) return this.bmiImages.underweight;
      else if (this.bmi < 24.9) return this.bmiImages.normal;
      else if (this.bmi < 29.9) return this.bmiImages.overweight;
      else if (this.bmi < 34.9) return this.bmiImages.obese1;
      else if (this.bmi < 39.9) return this.bmiImages.obese2;
      else return this.bmiImages.obese3;
    },

    showTipTool() {
      return this.tips[this.showTipToolIndex];
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
    },

    tiptool() {
      this.showTip = !this.showTip;
      if (this.showTip) {
        this.showTipToolIndex = (this.showTipToolIndex + 1) % this.tips.length;
      }
    }
  }
};
</script>