    <template>
        <div class="rounded container bg-secondary text-light ">
        <div class="mb-3 row">
            <div class="col-sm-10">
            <input type="text" class="form-control" id="surveyTitle" v-model="surveyTitle" placeholder="설문 제목 입력"/>
            </div>
        </div>
    
        <div class="mb-3 row">
            <div class="col-sm-10">
            <textarea class="form-control" id="surveyDescription" v-model="surveyDescription" placeholder="설명 입력"></textarea>
            </div>
        </div>
    
        <div class="mb-3 row">
            <label for="surveyStartDate" class="col-sm-2 col-form-label">설문 기간:</label>
            <div class="col-sm-5">
            <input type="date" class="form-control" id="surveyStartDate" v-model="surveyStartDate" /> 부터
            </div>
            <div class="col-sm-5">
            <input type="date" class="form-control" id="surveyEndDate" v-model="surveyEndDate" /> 까지
            </div>
        </div>
        </div>
    </template>
    
    <script>
    export default {
        data() {
        return {
            surveyTitle: '', // 제목 데이터
            surveyDescription: '', // 설명 데이터
            surveyStartDate: '', // 설문 시작일 데이터
            surveyEndDate: '' // 설문 종료일 데이터
        };
        }
    };
    </script>
    
    <style scoped>
    </style>
    