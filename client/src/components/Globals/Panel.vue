<template>
  <v-card flat>
    <v-card
      class="mx-auto"
      :height="height"
      :max-width="maxWidth"
    >
      <v-toolbar color="blue lighten-3" flat>
        <v-toolbar-title style="color: white">{{ title }}</v-toolbar-title>
        <slot name="extension"/>
      </v-toolbar>
      <v-divider></v-divider>
      <v-card-text>
        <slot>
          No slot content defined.
        </slot>
      </v-card-text>
    </v-card>
  </v-card>
</template>

<script>
export default {
  props: [
    'title',
    'maxWidth',
    'height'
  ]
}
</script>

<style scoped>
</style>
