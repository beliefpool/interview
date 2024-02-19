<script setup>
import { ref, computed, onMounted } from "vue";
import axios from "axios";

var tableData = ref([]);

async function getData() {
  // 请求数据
  try {
    var response = await axios.get("../../public/data/data.json");
    tableData.value = response.data.data;
    addAvg()
  } catch (error) {
    console.error("this is error", error);
  }
}
function addAvg() {
  // 添加平均分属性并给其赋值
  for (let i = 0; i < tableData.value.length; i++) {
    let count = 0.00;
    tableData.value[i].avgPrice = computed(() => {
      for (let j = 0; j < tableData.value[i].reviews.length; j++) {
        count = count + tableData.value[i].reviews[j].rating;
      }
      return (count / tableData.value[i].reviews.length).toFixed(1);
    });
  }
  // console.log(tableData);
}

onMounted(() => {
  getData();
});
</script>

<template>
  <div class="contain">
    <el-table :data="tableData" border style="width: 100%">
      <el-table-column prop="name" label="名称" width="180" />
      <el-table-column prop="price" label="价格" width="180" />
      <el-table-column prop="avgPrice" label="平均评分" />
    </el-table>
  </div>
</template>

<style scoped>
.contain {
  display: flex;
  justify-content: center;
}
</style>
