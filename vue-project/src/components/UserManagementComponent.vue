<script setup>
import { ref, reactive, onMounted, computed } from "vue";
import axios from "axios";
import { ElTable } from "element-plus";

var tableData = reactive({});
// const sortedItems = reactive([])
const DataList = reactive({});//用来存储转换时间戳的变量

function handleClick() {
  console.log("click");
}

async function getData() {
  // 请求数据
  try {
    var response = await axios.get("../../public/data/data4.json");
    tableData.value = response.data.data;
    DataList.value = response.data.data;
    changData(tableData.value);
    // timeFiler()
    forData(DataList.value)
    groupData(DataList.value)
    changData(DataList.value);
    tableData.value = DataList.value
  } catch (error) {
    console.error("this is error", error);
  }
}

// 转化成时间戳
function timeFiler(val) {
  const date = new Date(val);
  return date.getTime();
}
function forData(val1) {
  for (let i = 0; i < val1.length; i++) {
    val1[i].registrationDate = timeFiler(val1[i].registrationDate);
  }
}

// 自定义排序方法
function groupData(list){
  let temp = {}
  for(let i =0;i<list.length;i++){
    for(let j =i+1;j<list.length;j++){
      let cha = list[i].registrationDate - list[j].registrationDate
      if(cha < 0){
        temp = list[i]
        list[i] = list[j]
        list[j] = temp
        // console.log(cha);
      }
    }
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
      value1[i].registrationDate = filter(value1[i].registrationDate);
    }
  }
}

// 弹出框
const dialogVisible = ref(false);

onMounted(() => {
  getData();
});
</script>

<template>
  <div>
    <el-table
      :data="tableData.value"
      :default-sort="{ prop: 'registrationDate', order: 'descending' }"
      style="width: 100%"
      type="index"
    >
      <el-table-column fixed prop="username" label="用户名" width="220" />
      <el-table-column prop="email" label="邮箱" width="220" />
      <el-table-column prop="registrationDate" label="注册日期" width="220" />
      <el-table-column prop="status.description" label="状态" width="220" />
      <el-table-column fixed="right" label="操作" width="280">
        <template #default="{ row, $index }">
          <el-button link type="primary" size="small" @click="handleClick"
            >编辑</el-button
          >
          <el-button
            link
            type="primary"
            size="small"
            @click="dialogVisible = true"
            >删除</el-button
          >
          <el-dialog v-model="dialogVisible" title="Tips" width="500">
            <span>你确定要删除吗？</span>
            <template #footer>
              <div class="dialog-footer">
                <el-button @click="dialogVisible = false">退出</el-button>
                <el-button type="primary" @click="dialogVisible = false">
                  确定
                </el-button>
              </div>
            </template>
          </el-dialog>
          <el-switch
            v-model="row.code"
            class="mb-2"
            active-text="启动"
            inactive-text="禁用"
          />
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<style scoped></style>
