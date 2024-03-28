<script setup>
//import HelloWorld from './components/HelloWorld.vue'
//import TheWelcome from './components/TheWelcome.vue'
//import MJ from './components/MJ.vue'
//import Bmi from './components/Bmi.vue'
import BmiPop from './components/BmiPop.vue'
// import 해올 때 밑의 header나 main에 <파일명 />이렇게 추가를 해야 선언해올 수 있음

import { ref } from 'vue';

const logoSrc = ref('./assets/profile.png');

const updateLogo = (event) => {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = () => {
      logoSrc.value = reader.result;
    };
    reader.readAsDataURL(file);
  }
};
</script>


<template>
 
 <header>
    <div class="picture-container">
      <div class="picture">
        <label for="picture-choose">
          <img src="./assets/profile.jpeg" class="border border-dark border-2 picture-src" id="pictureChoose" title="프로필 사진을 선택하세요">
        </label>
        <input type="file" id="picture-choose" ref="fileInput" style="display: none;" @change="updateLogo">
      </div>
      <h6 class="text-center">프로필 사진 선택</h6>
    
    </div>
    <!--<img alt="Vue logo" class="logo" src="./assets/logo.png" width="200" height="200" />-->
    <!--<img alt="Vue logo" class="logo border border-dark border-2 rounded-circle" src="./assets/bmilogo.png" width="200" height="200" />
    -->

    <div class="wrapper">
      <!--<HelloWorld msg="You Can Do It!" />
      <MJ />
      <Bmi />-->
      <BmiPop />
    </div>
  </header>

  <main>
    <!--<TheWelcome />-->
  </main>
</template>

<style scoped>
.picture-container {
  text-align: center;
}

.picture {
  display: inline-block;
  position: relative;
}

.picture label {
  cursor: pointer;
}

.logo {
  width: 150px;
  height: 150px;
}

/* 파일 선택 부분을 동그랗게 만듭니다. */
.picture input[type="file"] {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
}
</style>
