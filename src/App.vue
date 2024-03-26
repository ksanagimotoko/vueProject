<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import MJ from './components/MJ.vue'
import Bmi from './components/Bmi.vue'
// import 해올 때 밑의 header나 main에 <파일명 />이렇게 추가를 해야 선언해올 수 있음
</script>


<template>
 
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.png" width="200" height="200" />

    <div class="wrapper">
      <HelloWorld msg="You Can Do It!" />
      <MJ />
      <Bmi />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
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
</style>
