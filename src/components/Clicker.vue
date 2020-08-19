<template>
  <div>
    <button @click="firstCounter++">You clicked me {{firstCounter}} times</button>
    <button @click="secondCounter++">You clicked me {{secondCounter}} times</button>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class Clicker extends Vue {
  private firstCounter: number = 0;
  private secondCounter: number = 0;
}
</script>

<style lang="scss" scoped>

</style>