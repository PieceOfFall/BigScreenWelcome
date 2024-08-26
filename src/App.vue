<script setup lang="ts">
import { onMounted, ref } from 'vue';
import Axios from 'axios';

/** 文字展示方法封装 */
const showDuration = 10 * 1000;
const showText = ref("")
let TextArr: Array<string> = []
const isErasingIn = ref(false);

const delay = (time: number) => new Promise(resolve => setTimeout(resolve, time))

const changeText = async (newText: string, showTime: number) => {
  showText.value = newText;
  isErasingIn.value = true;
  await delay(showTime);
  isErasingIn.value = false;
  await delay(1000);
}

/** 控制逻辑 */
const getText = async () => await Axios.get(`http://${import.meta.env.VITE_GET_URL}/get`);

onMounted(async () => {


  // eslint-disable-next-line no-constant-condition
  while (true) {
    const ret = await getText();
    TextArr = ret.data.data as Array<string>;
    for (let index = 0; index < TextArr.length; index++) {
      const element = TextArr[index];
      await changeText(element, showDuration)
    }
  }
})

</script>

<template>
  <div id="main-container">
    <div :class="['box', { erasingInEffect: isErasingIn }]">
      <div class="text">{{ showText }}</div>
    </div>
  </div>
</template>

<style scoped lang="scss">
#main-container {
  height: 100%;
  background-color: black;
  color: #3CC8FF;
  font-family: 'SourceHanSansCN';
  font-size: 50px;
  letter-spacing: 3px;

  position: absolute;
  top: 70px;
  right: 450px;

  .box {
    overflow: hidden;
  }

  .text {
    white-space: nowrap;
  }

  .erasingInEffect {
    width: 100%;
    animation: show 1s ease-in alternate;
  }

  @keyframes show {
    0% {
      width: 0%
    }

    100% {
      width: 100%;
    }
  }

}
</style>
