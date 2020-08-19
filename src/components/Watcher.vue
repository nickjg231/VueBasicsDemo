<template>
  <div>
    <p>
      Ask a question:
      <input v-model="message">
    </p>
    <button :disabled="disabled">Submit</button>
    <div v-show="disabled">Typing...</div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Watch } from 'vue-property-decorator';
import {debounce} from 'lodash';

@Component
export default class Watcher extends Vue {
  private message: string = '';
  private disabled: boolean = false;
  private debouncedGetAnswer: any;

  private created() {
    this.debouncedGetAnswer = debounce(() => this.disabled = false, 500);
  }

  @Watch('message')
  private onQuestionChange(newValue: string, oldValue: string) {
     this.disabled = true;
     this.debouncedGetAnswer();
  }
}
</script>

<style lang="scss" scoped>

</style>