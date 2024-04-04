<template>
  <div class="container-fluid" :style="{ backgroundColor: bgColor, height: '600px' }">
    <!--height 부분을 수정하면 색 넣는 부분을 더 늘리거나 줄일 수 있음-->
    <label for="exampleColorInput" class="form-label"> 배경색을 고르세요 </label>
    <input type="color" class="form-control form-control-color" id="exampleColorInput" value="#E5D3FD" title="Choose your color" @input="changeBgColor">
    <!--배경색 선택 할 수 있게 해줌-->
    <div>
    <input type="date" v-model="selectedDate">
    <input type="time" v-model="selectedTime">
    </div>
    <div class="row justify-content-center">
      <!--가운데 정렬-->
      <div class="col-md-6">
        <!--화면의 중간부분을 의미-->
        <h1 class="text-center">BMI 계산기</h1>
        <!--글씨 가운데로-->
        <form @submit.prevent="calculateBMI">
        <!--submit는 새로고침, prevent는 막는다는 뜻. calculateBmi를 불러오는데 새로고침은 되지 않도록함-->
          <div class="form-group"><!--입력 요소들을 그룹화한다-->
            <label for="height">키 (cm):</label>
            <input type="number" id="height" v-model.number="height" required class="form-control" placeholder="160">
            <!--number만 입력 가능, v-model.number은 입력값이 height에 입력한 값과 같게끔 해줌, required는 필수입력칸으로 만들어줌,
              placeholder은 예시: 홍길동 같은 느낌의 기능-->
          </div>
          <div class="form-group">
            <label for="weight">몸무게 (kg):</label>
            <input type="number" id="weight" v-model.number="weight" required class="form-control" placeholder="50">
          </div>
          <!-- BMI 계산 버튼 -->
          <button type="submit" class="btn btn-primary">BMI 계산하기</button>
          <!--submit 제출하기 기능-->
        </form>
      </div>
      <div class="col-md-6 result" v-if="bmi !== null">
        <h2>BMI:</h2>
        <p>{{ bmi.toFixed(2) }}</p>
        <p>{{ BMICategory(bmi) }}</p>
        <img class="bmi--img" v-if="selectImg === '../assets/low.jpeg'" src='../assets/low.jpeg'>
        <img class="bmi--img" v-else-if="selectImg === '../assets/normal.jpeg'" src='../assets/normal.jpeg'>
        <img class="bmi--img" v-else-if="selectImg === '../assets/high.jpeg'" src='../assets/high.jpeg'>
        <img class="bmi--img" v-else-if="selectImg === '../assets/danger.jpeg'" src='../assets/danger.jpeg'>
        <!--이미지를 이렇게 표현하지 않으면 전부 에러가 나거나 노출이 안됨.방법을 찾아봐야겠음-->
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
      selectedDate: '',
      selectedTime: ''
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
        return '../assets/low.jpeg.';
      } else {
        return '../assets/low.jpeg.';
      }
    },
    changeBgColor(event) {
      this.bgColor = event.target.value;
    }
    //사용하는 사람이 배경색을 선택 할 수 있도록 해줌
  }
};
</script>
