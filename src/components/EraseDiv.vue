<template>
    <div class="erase-container">
        <div class="erase-mask" ref="mask">
            <slot />
        </div>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const mask = ref(null);

const eraseDiv = () => {
    if (mask.value) {
        mask.value.animate([
            { width: '0%' },
            { width: '100%' }
        ], {
            duration: 2000, // 2 seconds
            fill: 'forwards'
        });
    }
};

onMounted(() => {
    eraseDiv();
});
</script>

<style scoped>
.erase-container {
    height: 100%;
    position: relative;
    overflow: hidden;
}

.erase-mask {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(to right, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 1) 100%);
}
</style>