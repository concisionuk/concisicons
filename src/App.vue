<template>
  <div id="canvas" :class="`theme-${active}`">
    <img alt="Vue logo" src="@/assets/logo.png" />
    <ColorModeToggle
      v-model="active"
      class="color-mode-toggle"
      :modes="modes"
    />
  </div>
</template>

<script lang="ts">
import ColorModeToggle from '@/components/color-mode-toggle.vue'

export default {
  name: 'App',
  components: {
    ColorModeToggle,
  },
  data: () => ({
    modes: ['system', 'dark', 'light'],
    active: 'system',
  }),
}
</script>

<style lang="scss">
html,
body {
  margin: 0;
  padding: 0;
  height: 100vh;
  overflow: hidden;
}
#canvas {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  width: 100%;
  height: 100vh;

  &.theme {
    &-dark {
      background: #2c3e50;
      color: white;
    }
    &-system {
      background: green;
      color: white;
    }
  }

  .color-mode-toggle {
    display: block;
    color: inherit;
    margin: 1rem auto;
    background: none;
    border: none;
    font-size: 1.5rem;
    outline: none;
  }
}
</style>
