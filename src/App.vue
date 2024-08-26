<script setup lang="ts">
import { onMounted, ref } from 'vue';

/** 文字展示方法封装 */
const showDuration = 10 * 1000;
const showText = ref("")
const isErasingIn = ref(false);

const delay = (time: number) => new Promise(resolve => setTimeout(resolve, time))

const changeText = async (newText: string, showTime: number) => {
  isErasingIn.value = false;
  await delay(1000);
  showText.value = newText;
  isErasingIn.value = true;
  await delay(showTime);
}

/** 控制逻辑 */
onMounted(async () => {
  // eslint-disable-next-line no-constant-condition
  while (true) {
    await changeText("豫章故郡，洪都新府。星分翼轸，地接衡庐。", showDuration)
    await changeText("襟三江而带五湖,控蛮荆而引瓯越。物华天宝,龙光射牛斗之墟。", showDuration)
    await changeText("人杰地灵，徐孺下陈蕃之榻。雄州雾列，俊采星驰。", showDuration)
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
  right: 450cqb;

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
