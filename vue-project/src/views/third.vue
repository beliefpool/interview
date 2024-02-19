<script setup>
import { ref, computed, onMounted } from "vue";
import axios from "axios";

var tableData = ref([]);
var sponData = ref([]);
const parentBorder = ref(false);
const childBorder = ref(false);
// 分页
const currentPage4 = ref(1);
const pageSize4 = ref(5);
const small = ref(false);
const background = ref(true);
const disabled = ref(false);
const total = ref(0);

const handleSizeChange = (val) => {
  // console.log(`${val} items per page`);
  pageSize4.value = val;
  const start = (currentPage4.value - 1) * val;
  const end = start + val;
  tableData.value = sponData.value.slice(start, end);
};
const handleCurrentChange = (val) => {
  // console.log(`current page: ${val}`);
  currentPage4.value = val;
  const start = (val - 1) * pageSize4.value;
  const end = start + pageSize4.value;
  tableData.value = sponData.value.slice(start, end);
};
function pageData(data) {
  const start = (currentPage4.value - 1) * pageSize4.value;
  const end = start + pageSize4.value;
  // console.log(end, start);
  return data.slice(start, end);
}

async function getData() {
  // 请求数据
  try {
    var response = await axios.get("../../public/data/data2.json");
    sponData.value = response.data.data;
    // tableData.value = sponData.value;
    tableData.value = pageData(sponData.value);
    changData(tableData.value);
    total.value = sponData.value.length;
    getOptions()
  } catch (error) {
    console.error("this is error", error);
  }
}

function filter(value) {
  // 转化时间函数
  if (value) {
    const date = new Date(value);
    return date.toLocaleString();
  }
  return value;
}
function changData(value1) {
  // 遍历数据
  if (value1) {
    for (let i = 0; i < value1.length; i++) {
      for (let j = 0; j < value1[i].users.length; j++) {
        value1[i].users[j].createdAt = filter(value1[i].users[j].createdAt);
        // console.log(value1[i].users[j].createdAt);
      }
    }
  }
  return value1;
}

// 筛选器
const value = ref('')
const options = ref([])

function getOptions(){
  // 弄出options
  const con = []
  let son = []
  for(let i =0;i<sponData.value.length;i++){
    if(sponData.value[i].groupName){
      con.push(sponData.value[i].groupName)
    }
  }
  // console.log(con);
  son = [...new Set(con)]
  for(let i =0;i<son.length;i++){
    options.value.push({value:son[i],label:son[i]})
  }
  // console.log(options.value);
}
function selectData(){
  // 筛选数据
  let dataN = []
  for(let i =0;i<sponData.value.length;i++){
    if(sponData.value[i].groupName === value.value){
      dataN.push(sponData.value[i])
    }
  }
  sponData.value = dataN
  total.value = sponData.value.length
  // console.log(sponData.value);
}

onMounted(() => {
  getData();
});
</script>

<template>
  <div>
    <el-select v-model="value" placeholder="Select" style="width: 240px">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
        :disabled="item.disabled"
        @click="selectData()"
      />
    </el-select>
    <el-table :data="tableData" :border="parentBorder" style="width: 100%">
      <el-table-column type="expand">
        <template #default="props">
          <div m="4">
            <el-table :data="props.row.users" :border="childBorder">
              <el-table-column label="用户名" prop="name" />
              <el-table-column label="邮箱" prop="email" />
              <el-table-column label="角色" prop="role" />
              <el-table-column label="创建时间" prop="createdAt" />
            </el-table>
          </div>
        </template>
      </el-table-column>
      <el-table-column label="GroupId" prop="groupId" />
      <el-table-column label="GroupName" prop="groupName" />
    </el-table>
    <div class="demo-pagination-block">
      <el-pagination
        v-model:current-page="currentPage4"
        v-model:page-size="pageSize4"
        :page-sizes="[5, 10, 15, 20]"
        :small="small"
        :disabled="disabled"
        :background="background"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
      />
    </div>
  </div>
</template>

<style scoped>
.demo-pagination-block {
  margin-top: 10px;
  display: flex;
  justify-content: center;
}
.demo-pagination-block .demonstration {
  margin-bottom: 16px;
}
</style>
