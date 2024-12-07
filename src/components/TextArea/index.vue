<script setup lang="ts">

import { ref, onMounted } from 'vue';

const textarea = ref('');
const inputRef = ref<HTMLDivElement | null>(null);

onMounted(() => {
  inputRef.value?.setAttribute('data-placeholder', '请输入...');

});


const inputMessage = () => {
  textarea.value = inputRef.value?.textContent || '';
  if (textarea.value === '') {

    (inputRef.value as HTMLDivElement).innerHTML = '';
  }
};


</script>

<template>


  <div class="ai-semantic-recognition-container-tool-input">
    <div ref="inputRef" class="ai-semantic-recognition-container-tool-input-left" contenteditable="true"
         @input="inputMessage" />

    <div class="ai-semantic-recognition-container-tool-input-right">
      <img width="16" src="./assets/sendIcon.png" alt="sendIcon">
      发送
    </div>
  </div>


</template>

<style scoped lang="scss">


.ai-semantic-recognition-container-tool-input {
  height: calc(100% - 50px);
  position: relative;
  width: 100%;
  transform: translateX(0); //设置了这个后，里面button就相对于父类 进行fixed定位
  border-radius: 4px;
  outline: 1px solid;
  outline-image: linear-gradient(284deg, #FFCAB1 0%, #8CCEE3 54%, #06C6FF 100%) 0.5;
  outline-image-slice: 1;
  background: rgba(255, 255, 255, 0.05);

  &-left {
    text-align: left;
    padding: 15px;
    width: calc(100% - 5% - 100px);
    height: 100%;
    box-sizing: border-box;
    overflow-y: auto;
    font-size: 14px;
    white-space: pre-wrap; /* 保持换行 */
    word-wrap: break-word; /* 防止单词撑破盒子 */
    overflow-wrap: break-word; /* 防止长单词溢出 */

    &:empty::before {
      content: attr(data-placeholder);
      pointer-events: none; /* 防止占位符被点击 */
      display: block;
      height: 32px;
      color: rgba(255, 255, 255, 0.2);
    }

  }

  &-right {
    position: fixed;
    right: 5%;
    top: 25%;
    width: 80px;
    height: 28px;
    box-sizing: border-box;
    padding: 4px 12px;
    background: linear-gradient(112deg, #FFAB84 -4%, #20B7EA 60%, #6DDBFF 100%);
    box-shadow: 0 4px 10px 0 rgba(0, 0, 0, 0.3);
    border-radius: 4px;
    text-align: center;
    line-height: 20px;
    font-size: 14px;
  }

}


</style>