<template>
    <div id="app">
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-md-6">
                    <h2 class="title mt-5 mb-4 text-center"> BMI 계산기 </h2>
                    <div class="form-group">
                        <label for="height"> 키(cm) : </label>
                        <input type="number" class="form-control" id="height" v-model="height">
                    </div>

                    <div class="form-group">
                        <label for="weight"> 몸무게(kg) : </label>
                        <input type="number" class="form-control" id="weight" v-model="weight">
                    </div>

                    <div class="row">
                        <div class="col-md-6">
                            <button @click="calculateBMI" class="btn btn-primary btn-block btn-bmi">
                                BMI 계산하기 
                            </button>
                        </div>
                        <div class="col-md-6">
                            <button @click="resetBMI" class="btn btn-primary btn-block btn-bmi"> BMI 초기화 </button>
                        </div>
                    </div>

                    <div class="row justify-content-center">
                        <div class="col-md-6 text-center">
                            <div class="btn-group btn-group-toggle" data-toggle="buttons">
                                <label class="btn btn-secondary btn-operation" @click="calculateOperation('plus')">
                                    <input type="radio" name="options" id="opt1"> +
                                </label>
                                <label class="btn btn-secondary btn-operation" @click="calculateOperation('minus')">
                                    <input type="radio" name="options" id="opt2"> -
                                </label>
                                <label class="btn btn-secondary btn-operation" @click="calculateOperation('multiply')">
                                    <input type="radio" name="options" id="opt3"> x
                                </label>
                                <label class="btn btn-secondary btn-operation" @click="calculateOperation('divide')">
                                    <input type="radio" name="options" id="opt4"> ÷
                                </label>
                            </div>
                        </div>
                        <div class="col-md-6 text-center">
                            <button @click="resetOperation" class="btn btn-primary btn-block"> 사칙연산 초기화 </button>
                        </div>
                    </div>

                    <div class="result row justify-content-center mt-4" v-if="result !== null">
                        <div class="col-md-6">
                            <div class="card">
                                <div class="card-body">
                                    <h4> 사칙연산 결과: {{ result }} </h4>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="result row justify-content-center mt-4" v-if="bmi !== null">
                    <div class="col-md-6">
                        <div class="card">
                            <div class="card-body">
                                <h4> 당신의 BMI는 {{ bmi }}, {{ bmiCategory() }} 입니다. </h4>
                                <img :src="bmiImage()" alt="BMI Image" class="bmi-image">
                            </div>
                        </div>
                    </div>
                
                </div>
            </div>
        </div>
    </div>
</template>

<style>
 .btn-operation {
    width: calc(25% - 5px);
}

.btn-bmi {
    width: calc(50% - 5px);
}
</style>


<script setup>

import { ref, computed } from 'vue';
import underweightImage from '@/assets/bmiImages/under.png';
import normalImage from '@/assets/bmiImages/normal.png';
import overweightImage from '@/assets/bmiImages/over.png';
import obese1Image from '@/assets/bmiImages/ob1.png';
import obese2Image from '@/assets/bmiImages/ob2.png';
import obese3Image from '@/assets/bmiImages/ob3.png';

const height = ref(null);
const weight = ref(null);
const bmi = ref(null);
const result = ref(null);

const bmiImages = {
    underweight: underweightImage,
    normal: normalImage,
    overweight: overweightImage,
    obese1: obese1Image,
    obese2: obese2Image,
    obese3: obese3Image
};

const calculateBMI = () => {
    if (height.value && weight.value) {
        const heightMeter = height.value / 100 ;
        bmi.value = ( weight.value / (heightMeter * heightMeter)).toFixed(2);
    } else {
        alert('키와 몸무게를 입력하세요.');
    }
};

const calculateOperation = ( operation ) => {
    if (height.value && weight.value) {
        const heightMeter = height.value / 100 ;
        switch (operation) {

            case 'plus':
                result.value = (parseFloat(weight.value) + parseFloat(height.value)).toFixed(2);
                break;
            case 'minus':
                result.value = (parseFloat(weight.value) - parseFloat(height.value)).toFixed(2);
                break;
            case 'multiply':
                result.value = (parseFloat(weight.value) * parseFloat(height.value)).toFixed(2);
                break;
            case 'divide':
                result.value = ( parseFloat(weight.value) / parseFloat(heightMeter)).toFixed(2);
                break;
            default:
                break;
        }
    } else {
        alert('키와 몸무게를 입력하세요.');
    }
};

const resetBMI = () => {
        height.value = null;
        weight.value = null;
        bmi.value = null;
    };

const resetOperation = () => {
        result.value = null;
    };

const bmiCategory = ( ) => {
    if ( bmi.value === null ) return '';
    if ( bmi.value < 18.5 ) return '저체중';
    else if (bmi.value < 24.9) return '정상';
    else if (bmi.value < 29.9) return '과체중';
    else if (bmi.value < 34.9) return '경도비만';
    else if (bmi.value < 39.9) return '중도비만';
    else return '과도비만';
};

const bmiImage = ( ) => {
    if (bmi.value === null) return '';
    if (bmi.value < 18.5) return bmiImages.underweight;
    else if (bmi.value < 24.9) return bmiImages.normal;
    else if (bmi.value < 29.9) return bmiImages.overweight;
    else if (bmi.value < 34.9) return bmiImages.obese1;
    else if (bmi.value < 39.9) return bmiImages.obese2;
    else return bmiImages.obese3;

};


</script>