<!-- 추가 누를 때 마다 번호 부여되는 코드인데 좀 입력 칸이 큼,, 그리고 숫자 수정한다고 바뀌지 않음 방법을 찾아야함
  <script setup>
import { ref } from 'vue'
import MainDiv from './components/MainDiv.vue'
import EachSelect from './components/EachSelect.vue'

const eachSelects = ref([]);
let idCounter = 1;

const add = () => {
  eachSelects.value.push({ id: idCounter });
  idCounter++;
}

const changeId = (index, newId) => {
  eachSelects.value[index].id = newId;
}
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-md-auto ms-auto">
          <button @click="add" class="btn btn-primary">추가</button>
        </div>
      </div>
    </div>
    <div class="wrapper">
      <div class="container">
        <div class="row">
          <div class="col">
            <MainDiv />
          </div>
        </div>
        <div class="row" style="gap: 10px;">
          <div class="col-12" v-for="(eachSelect, index) in eachSelects" :key="index">
            <div>
              <input type="text" v-model="eachSelect.id" @input="changeId(index, eachSelect.id)" class="form-control" placeholder="ID" />
            </div>
            <EachSelect :id="eachSelect.id" />
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
.wrapper {
  display: flex;
  place-items: flex-start;
  flex-wrap: wrap;
}

.row {
  display: flex;
  flex-wrap: wrap;
}
</style>
-->
<script setup>
import { ref } from 'vue'
import MainDiv from './components/MainDiv.vue'
import EachSelect from './components/EachSelect.vue'

const eachSelects = ref([]);

const add = () => {
  eachSelects.value.push(EachSelect);
}
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="row align-items-center">
        <div class="col-md-auto ms-auto">
          <button @click="add" class="btn btn-primary">추가</button>
        </div>
      </div>
    </div>
    <div class="wrapper">
      <div class="container">
        <div class="row">
          <div class="col">
            <MainDiv />
          </div>
        </div>
        <div class="row" style="gap: 10px;">
          <div class="col-12" v-for="(eachSelect, index) in eachSelects" :key="index">
            <EachSelect />
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
.wrapper {
  display: flex;
  place-items: flex-start;
  flex-wrap: wrap;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

</style>


