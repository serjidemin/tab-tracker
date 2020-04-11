<template>
  <panel title="Tab">
    <v-textarea class="textarea"
                readonly
                v-model="tab"/>
  </panel>
</template>

<script>
export default {
  props: [
    'tab'
  ]
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
