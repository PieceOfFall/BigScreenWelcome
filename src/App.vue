<script setup lang="ts">
import { onMounted, ref } from 'vue';

/** 文字展示方法封装 */
const showDuration = 10 * 1000;
const showText = ref("")
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
onMounted(async () => {
  // eslint-disable-next-line no-constant-condition
  while (true) {
    await changeText("开发出老百姓用得起的高质量生物药", showDuration)
    await changeText("始于信，达于行", showDuration)
    await changeText("成为国际一流的生物制药公司", showDuration)
    await changeText("以创新为基石，走全球化道路", showDuration)
    await changeText("诚信、会学、肯干、协作", showDuration)
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
