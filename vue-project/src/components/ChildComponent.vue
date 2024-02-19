<script setup>
import { ref, reactive } from 'vue'
import axios from "axios";

const listData = ref({})

// 子组件接收数据
const praentData = defineProps({
    userDate:Object
});
// console.log(listData);

async function update(id){
    // 更新接口
    await axios.get('../../public/data/data3.json', {
    params: {
      ID: id
    }
  })
  .then(function (response) {
//    判断是否成功
    if(response.data.status == 'success'){
        // 从新获取用户列表数据
        axios
        .get("../../public/data/data3.json")
        .then(function(response) {
            listData.value = response.data;
        })
    }
  })
  .catch(function (error) {
    console.log(error);
  });
}


// console.log(praentData);
</script>

<template>
  <div>
    <div class="box" v-for="(item,index) in userDate" :key="item.id">
    <h3>姓名:{{ item.name}}</h3>
    <h3>邮箱:{{ item.email}}</h3>
    <h3>角色：{{ item.role }}</h3>
    <button @click="update(item.id)">更新</button>
  </div>
  </div>
</template>

<style scoped>

</style>