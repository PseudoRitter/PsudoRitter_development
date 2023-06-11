<script setup lang="ts">
import {reactive, ref } from 'vue'
defineProps<{ msg: string }>()

const header = ref('Калькулятор')

const originalNumber = ref() 
const resultNumber = ref()
const mathOperationNumber = ref ()
const picked = ref('')

const listNumbers =  reactive([ ])

function addData(){
  const newData =  { num: '', typeOperation: '', timeChange: '', result: '' }
  if(originalNumber.value != '' && picked.value != '' &&  mathOperationNumber.value != '' && resultNumber.value != ''){
    newData.num = originalNumber.value;
    newData.typeOperation = picked.value;
    newData.timeChange = mathOperationNumber.value;
    newData.result = resultNumber.value;
    listNumbers.push({...newData });
  }
  else{ 
    alert("Не все данные введены")
  }
}

function multiplyNumber(multiplier) {
  if(mathOperationNumber.value > 1)
  resultNumber.value = originalNumber.value * multiplier.value
}

function divisionNumber(divider) {
  if(mathOperationNumber.value > 1)
    resultNumber.value = originalNumber.value / divider.value
}

function countNumber() {
  if (picked.value == 'Multiply'){
    return multiplyNumber(mathOperationNumber)
  } else if (picked.value == 'Division'){
    return divisionNumber(mathOperationNumber)
  }
}
</script>

<template>
  <h1>{{ header }}</h1>
  
  <p> Изначальное число: 
    <input v-model.number="originalNumber" type='number' min='1' placeholder="Введите число"/>
  </p>
  <p> Введите кратность, на которую хотите увеличить число: 
    <input v-model.number="mathOperationNumber" type='number' min='1' placeholder="Введите число"/>
  </p>
  <!-- <p> <button type="button" @click="multiplyNumber">Увеличить в колличество раз: {{ mathOperationNumber }}</button> </p>
  <p> <button type="button" @click="divisionNumber">Уменьшить в колличество раз: {{ mathOperationNumber }}</button> </p> -->
  <div>Выберете операцию: </div>
	<input type="radio" id="multiply" value="Multiply" v-model="picked" />
	<label for="multiply">Умножить</label>

	<input type="radio" id="division" value="Division" v-model="picked" />
  <label for="division">Разделить</label>

  <p> <button type="button" @click="countNumber(), addData()" > Посчитать </button></p>
  <p> Получившееся число: {{ resultNumber}} </p>

  <p> История операций: </p>

  <table id='tableElements'>
    <thead>
      <tr>
        <th> #</th>
        <th>Изначальное число</th>
        <th>Тип операции</th>
        <th>Кратность изменения</th>
        <th>Результат</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in listNumbers" :key="index">
        <td> {{ index + 1 }}</td>
        <td> {{ item.num }}</td>
        <td> {{ item.typeOperation }}</td>
        <td> {{ item.timeChange }}</td>
        <td> {{ item.result }}</td>
        </tr>
    </tbody>
  </table>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>

