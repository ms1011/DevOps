<template>
  <div class="plus">
    <h1>덧셈 기능 만들기</h1>
    <label>num1: </label><input type="text" v-model="num1">&nbsp;
    <label>num2: </label><input type="text" v-model="num2">&nbsp;
    <button @click="sendPlus">더하기</button>
    <hr>
    <p>{{ num1 }} + {{ num2 }} = {{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const num1 = ref(0);
const num2 = ref(0);
const result = ref(0);

const sendPlus = async() => {
  // const response = await fetch(`http://localhost:7777/plus?num1=${num1.value}&num2=${num2.value}`);
  // const response = await fetch(`http://localhost:5173/api/plus?num1=${num1.value}&num2=${num2.value}`);  // Front에서 CORS 처리
  
  /* 백엔드를 도커 컨테이너로 8055 포트로 만들었을 때 */
  const response = await fetch(`http://localhost:8055/plus?num1=${num1.value}&num2=${num2.value}`);
  const data = await response.json();
  console.table(data);
  result.value = data.sum;
}

</script>

<style scoped>
  .plus {
    text-align: center;
  }
</style>