<template>
  <panel title="Tab">
    <v-textarea class="textarea"
                readonly
                v-model="tab"/>
  </panel>
</template>

<script>
import Panel from '@/components/Panel'

export default {
  props: [
    'tab'
  ],
  components: {
    Panel
  }
}
</script>

<style scoped>
  .textarea {
    font-size: 12px;
    font-family: monospace;
    border: none;
    height: 600px;
    border-color: transparent;
    overflow: auto;
    padding: 20px;
  }
</style>
