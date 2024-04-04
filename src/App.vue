<script setup>
import { ref } from 'vue';
import layout1 from './components/layout1.vue'
import TheWelcome from './components/TheWelcome.vue'

const layouts = ref([layout1]);
const layoutCounter = ref(1);

function addLayout() {
  layouts.value.push(layout1);
  layoutCounter.value++;
}
</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />-->

  </header>

  <main>
    <div class="btn">
      <button @click="addLayout"> 추가 </button>
      <div v-for="layout in layouts" :key="layoutCounter">
        <layout1 />
      </div>
    </div>
  </main>

</template>

<script setup>



</script>

<style scoped>

/* #nsv_root {
      margin: 0;
      height: 100%;
    }
     */
/* header {
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
} */
</style>
