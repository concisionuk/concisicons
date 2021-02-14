<template>
  <button
    role="button"
    aria-label="Toggle colour theme"
    class="themetoggler"
    :class="value"
    @click="cycleModes()"
  >
    <i class="themetoggler-icon">
      <span class="themetoggler-line a" />
      <span class="themetoggler-line b" />
      <span class="themetoggler-line c" />
      <span class="themetoggler-line d" />
      <span class="themetoggler-line e" />
      <span class="themetoggler-line f" />
    </i>
  </button>
</template>

<script>
export default {
  name: 'ColorModeToggle',
  props: {
    modes: {
      type: Array,
      default: () => ['system', 'dark', 'light'],
    },
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    cycleModes() {
      const currentIndex = this.modes.indexOf(this.value)
      const nextIndex = (currentIndex + 1) % this.modes.length
      this.$emit('input', this.modes[nextIndex])
    },
  },
}
</script>

<style lang="scss" scoped>
$ts: 0.5s;
.themetoggler {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5rem;

  // &:hover,
  // &:focus,
  // &:active {
  //   .themetoggler-icon {
  //     transform: scale(1.4);
  //   }
  //   .themetoggler-line {
  //     &.a {
  //       transform: scaleY(0.6);
  //     }
  //     &.b {
  //       transform: rotate(45deg) scaleY(0.6);
  //     }
  //     &:nth-child(4n + 2) {
  //       transform: rotate(90deg) scaleY(0.6);
  //     }
  //     &.d {
  //       transform: rotate(135deg) scaleY(0.6);
  //     }
  //   }
  // }

  &::after {
    display: none;
  }

  &-icon {
    $size: 1em;
    position: relative;

    display: flex;
    align-items: center;
    justify-content: center;
    width: $size;
    height: $size;

    background-color: transparent;
    border-radius: 100%;
    box-shadow: inset 4px -2px 0 20px currentColor;
    will-change: box-shadow, transform, border-radius;

    transition: transform $ts ease, box-shadow $ts, border-radius $ts;
  }

  &-line {
    position: absolute;
    top: -0.5em;
    bottom: -0.5em;

    display: block;
    width: 2px;
    border-radius: 1px;

    background: linear-gradient(
      currentColor 12%,
      transparent 12%,
      transparent 88%,
      currentColor 88%
    );
    will-change: transform;

    transition: transform $ts ease;

    content: '';

    &.b {
      transform: rotate(45deg);
    }
    &.c {
      transform: rotate(90deg);
    }
    &.d {
      transform: rotate(135deg);
    }
    &.e,
    &.f {
      transform: rotate(90deg) translateX(0.5rem) scale(0);
      background: currentColor;
    }
  }

  &.dark {
    .themetoggler {
      &-icon {
        box-shadow: inset 0.3em -0.2em 0 -0.1em currentColor;
        transform: scale(1.6);
      }
      &-line {
        &.a {
          transform: scaleY(0);
        }
        &.b {
          transform: rotate(45deg) scaleY(0);
        }
        &.c {
          transform: rotate(90deg) scaleY(0);
        }
        &.d {
          transform: rotate(135deg) scaleY(0);
        }
      }
    }
  }

  &.system {
    .themetoggler {
      &-icon {
        box-shadow: inset 0 0 0 2px currentColor;
        transform: scale(1.6, 1.2);
        border-radius: 3px;
      }
      &-line {
        &.a {
          transform: scaleY(0);
        }
        &.b {
          transform: rotate(45deg) scaleY(0);
        }
        &.c {
          transform: rotate(90deg) scaleY(0);
        }
        &.d {
          transform: rotate(135deg) scaleY(0);
        }
        &.e {
          transform: rotate(90deg) translateX(0.54em) scale(1.8, 0.15);
        }
        &.f {
          transform: rotate(90deg) translateX(0.6em) scale(0.8, 0.25);
        }
      }
    }
  }
}
</style>
