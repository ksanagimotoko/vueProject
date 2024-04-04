<template>
  <div id="app">
    <div class="container">
      <h1>{{ surveyTitle }}</h1>

      <label for="titleInput">제목:</label>
      <input type="text" id="titleInput" v-model="surveyTitleInput">

      <p>{{ surveyDescription }}</p>

      <label for="descriptionInput">설명:</label>
      <textarea id="descriptionInput" v-model="surveyDescriptionInput"></textarea>
    </div>

  </div>
</template>

<script setup>
import { watch } from "vue";


const surveyTitle = '설문제목';
const surveyDescription = '설문 내용';
const surveyTitleInput = '';
const surveyDescriptionInput = '';

watch(() => surveyTitle, (newTitle) => {
  surveyTitle.value = newTitle;
});

watch(()=> surveyDescription, (newDescription) => {
  surveyDescription.value = newDescription
});

</script>

<style>
.container {
  width: 400px;
  height: 200px;
  background-color: red;
  border-radius: 20px;
}
</style>