<template>
    <div class="rounded container bg-secondary text-light ">
        <div class="mb-3 row">
            <label for="surveyTitle" class="col-sm-2 col-form-label">제목(다중선택):</label>
            <div class="col-sm-10">
                <input type="text" class="form-control" id="surveyTitle" v-model="surveyTitle" />
            </div>
        </div>
        <div v-for="(option, index) in options" :key="index">
            <div>
                <input type="checkbox" :value="option" v-model="selectedOptions" />
                {{ option }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            surveyTitle: '', // 직접 제목 입력
            options: ['옵션 1', '옵션 2', '옵션 3'], // 객관식 옵션
            selectedOptions: [] // 선택된 옵션들을 담을 배열
        };
    }
};
</script>
