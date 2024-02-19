<script setup>
import { ref, reactive, onMounted } from 'vue'
import axios from "axios";
import child from "./ChildComponent.vue";

let Data = ref({});
async function getData() {
  // 请求数据
  try {
    var response = await axios.get("../../public/data/data3.json");
    Data.value = response.data.data
    // console.log(Data);
  } catch (error) {
    console.error("this is error", error);
  }
}

onMounted(() => {
  getData();
});
</script>

<template>
  <div>
    <child :userDate="Data"></child>
  </div>
</template>

<style scoped>

</style>