<template>
    <div>
    <div class="greeting">Hello, {{ myName }}!</div>
    <div v-for="(data,index) in testVfor" :key="index">{{ data }}</div>
    </div>
</template>
<style>
.greeting {
    font-size: 24px;
    color: skyblue;
}
</style>
<script>
export default {
    data() {
    return {
        myName: 'MinJi',
        testVfor: ['25세','척척석사','개발 공부 중']
    };
    }
}
</script>