<template>
  <div>
    <input v-model="message">
    <p>Message: {{message}}</p>
    <p>Reverse: {{reverseMessage}}</p>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class ReverseText extends Vue {
  private message: string = '';

  private get reverseMessage(): string {
    return this.message.split('').reverse().join('');
  }
}
</script>

<style lang="scss" scoped>

</style>