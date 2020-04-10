<template>
  <panel title="YouTube Video">
    <youtube
      :video-id="youtubeId"
      player-width="100%"
      player-height="185px"></youtube>
  </panel>
</template>

<script>
import Panel from '@/components/Panel'

export default {
  props: [
    'youtubeId'
  ],
  components: {
    Panel
  }
}
</script>

<style scoped>
</style>
