<script setup>
import BMICalculator from './BMI/BMICalculator.vue';

</script>

<template>
  <header>
   <!--
   <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You 99999did it!" />
    </div>
    -->
  </header>

  <main>
    <BMICalculator />
  </main>

</template>

<style scoped>

#app {
  display: block;
  line-height: 3;
}
/*
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} 
*/
</style>
