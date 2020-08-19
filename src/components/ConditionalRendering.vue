<template>
  <div class="conditional-rendering">
    <div>
      <div v-if="isRendered">Rendered</div>
      <button @click="isRendered = !isRendered">Toggle Rendered</button>
    </div>
    <div>
      <div v-show="isShown">Shown</div>
      <button @click="isShown = !isShown">Toggle Shown</button>
    </div>
    <div>
      <div v-if="multipleConditionsValue === 0">First Condition</div>
      <div v-else-if="multipleConditionsValue === 1">Second Condition</div>
      <div v-else>Third Condition</div>
      <button @click="multipleConditionsValue = (multipleConditionsValue + 1) % 3">Toggle Condition</button>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class ConditionalRendering extends Vue {
  private isRendered: boolean = true;
  private isShown: boolean = true;
  private multipleConditionsValue: number = 0;
}
</script>

<style lang="scss" scoped>
.conditional-rendering > div {
  margin-bottom: 24px;
}
</style>


<template>
  <div class="conditional-rendering">
    <div>
      <div v-if="isRendered">Rendered</div>
      <button @click="isRendered = !isRendered">Toggle Rendered</button>
    </div>
    <div>
      <div v-show="isShown">Shown</div>
      <button @click="isShown = !isShown">Toggle Shown</button>
    </div>
    <div>
      <div v-if="multipleConditionsValue === 0">First Condition</div>
      <div v-else-if="multipleConditionsValue === 1">Second Condition</div>
      <div v-else>Third Condition</div>
      <button @click="multipleConditionsValue = (multipleConditionsValue + 1) % 3">Toggle Condition</button>
    </div>
  </div>
</template>

export default class ConditionalRendering extends Vue {
  private isRendered: boolean = true;
  private isShown: boolean = true;
  private multipleConditionsValue: number = 0;
}