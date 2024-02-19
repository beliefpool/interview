<script setup>
import { ref, onMounted } from "vue";

const msg = ref('1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。1..container元素是一个具有固定宽度且自适应高度的居中容器，其背景颜色为浅灰色。当浏览器窗口尺寸改变时，容器的高度需要保持与内容区域（.content）相同，但不超过屏幕高度的80%。')

</script>

<template>
  <div>
    <div class="container">
      <div class="content">
        {{ msg }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.container{
  width: 600px;
  max-height: 80vh;
  background-color: rgb(164, 161, 161);
  margin: 0 auto;
  display: flex;
  overflow: auto;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
.content{
  width: 100%;
  height: auto;
  transition: 0.5s ease;
  font-size: 16px;
  padding: 10px;
  box-sizing: border-box;
  text-align: left;
}
</style>
