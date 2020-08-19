<template>
  <div>
    <div :style="{ fontSize: fontSizePx + 'px' }">font size: {{fontSizePx}}px</div>
    <button @click="increaseFontSize">Increase font size</button>
    <button @click="fontSizePx = 10">Reset</button>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class FontSize extends Vue {
  private fontSizePx = 10;

  private increaseFontSize() {
    const fontIncrease = Math.floor(this.fontSizePx * 0.1);
    this.fontSizePx += fontIncrease;
  }
}
</script>

<style lang="scss" scoped>

</style>