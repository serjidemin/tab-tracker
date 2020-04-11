<template>
  <panel title="Lyrics">
    <v-textarea class="textarea"
                readonly
                v-model="lyrics"/>
  </panel>
</template>

<script>
export default {
  props: [
    'lyrics'
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
