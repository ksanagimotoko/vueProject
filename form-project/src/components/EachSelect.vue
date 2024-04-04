<template>
    <div class="rounded container bg-secondary text-light ">
        <div class="mb-3 row">
            <div class="col-sm-10">
                <input type="text" class="form-control" id="surveyTitle" v-model="surveyTitle" placeholder="질문 제목 입력" />
            </div>
        </div>
        <div v-for="(option, index) in options" :key="index">
            <div>
                <input type="radio" :value="option" v-model="selectedOption" />
                {{ option }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            surveyTitle: '', // 설문 제목 입력
            options: ['옵션 1', '옵션 2', '옵션 3'], // 객관식 옵션
            selectedOption: '' // 선택된 옵션
        };
    }
};
</script>
