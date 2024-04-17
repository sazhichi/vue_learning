<template>
  <!-- HTML-->
  <div>
    <ul>
      <li v-for="(item,index) in message_list" :key="index">
        {{item}}
      </li>
    </ul>
    <input v-model="input_message"/>
    <button @click="handleClick()">点击我</button>
  </div>
</template>



<script setup>
import {ref} from "vue";

const message_list = ref([]);

const input_message = ref(null);

const handleClick = () =>{
  message_list.value.push(input_message.value);
};
</script>


<style scoped>
</style>