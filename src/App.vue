<template>
  <!-- HTML-->
  <div>
    <a-list item-layout="horizontal" :data-source="messageList"><!--列表元素-->
      <template #renderItem="{ item }">
        <a-list-item>
          {{ item.username }}: {{ item.message }}
        </a-list-item>
      </template>
      <template #header>
        <div>
          消息列表
        </div>
      </template>
    </a-list>
    <a-row style="margin-top: 20px">
      <a-col span="4"><!--span+offset == 24-->
        <a-input v-model:value="username" placeholder="用户名">
          <template #prefix>
            <UserOutlined />
          </template>
        </a-input>
      </a-col>
      <a-col span="14" offset="1">
        <a-input v-model:value="message" placeholder="要输入的文本" >
          <template #prefix>
            <MessageOutlined />
          </template>
        </a-input>
      </a-col>
      <a-col span="4" offset="1"> 
        <a-button type="primary" @click="handleClickSubmit"style="width: 100%">提交</a-button>
      </a-col>
    </a-row>
  </div>
</template>



<script setup>
import { ref } from "vue";
import { MessageOutlined } from "@ant-design/icons-vue";
import { UserOutlined } from "@ant-design/icons-vue";
import axios from "axios";
import { message as ant_message } from "ant-design-vue";
const username = ref(null);
const message = ref(null);

const messageList = ref([]);
//按下提交按钮
const handleClickSubmit = async () =>{
  try{
    const res = (
        await axios.request({
        url: "http://localhost:8080/message/send",
        method: "POST",
        data:{
          username: username.value,
          message: message.value,
        },
     })
    ).data;
    if(res.status == 200) {
      ant_message.success("提交成功!");
    }
  }catch(err){
    ant_message.error("提交失败!"); 
  }finally{
    GetMessageList();
  }
};

//获取消息列表
const GetMessageList = async() =>{
  const res = (
    await axios.request({
        url: "http://localhost:8080/message/send",
        method: "GET",
        params: {},
     })
    ).data;
    messageList.value = res;
};
GetMessageList();

</script>


<style scoped>
</style>