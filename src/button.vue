<template>
  <button class="f-button kobe-gigi" :class="{[`icon-${iconPosition}`]: true}" @click="$emit('click')">
    <f-icon :name="icon" v-if="icon && !loading" class="icon"></f-icon>
    <f-icon name="loading" v-if="loading" class="icon loading"></f-icon>
    <div class="content">
      <slot></slot>
    </div>
  </button>
</template>

<script>
//import Vue from 'vue'
import Icon from "./icon";
//Vue.component('f-icon', Icon)
export default {
    components: {
    "f-icon": Icon
  },
  props: {
    icon: {},
    loading: {
      type: Boolean,
      default: false
    },
    iconPosition: {
      type: String,
      default: "left",
      validator(value) {
        return value === "right" || value === "left";
      }
    }
  }
};
</script>


<style lang="scss">
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.f-button {
  font-size: var(--font-size);
  height: var(--button-height);
  padding: 0 1em;
  border-radius: var(--border-radius);
  border: 1px solid var(--border-color);
  background: var(--button-bg);
  display: inline-flex;
  justify-content: center;
  align-items: center;
  vertical-align: middle;
  &:hover {
    border-color: var(--border-color-hover);
  }
  &:active {
    background: var(--button-active-bg);
  }
  &:focus {
    outline: none;
  }
  > .icon {
    order: 1;
    margin-right: 0.3em;
  }
  > .content {
    order: 2;
  }
  &.icon-right {
    > .icon {
      order: 2;
      margin-left: 0.3em;
      margin-right: 0;
    }
    > .content {
      order: 1;
    }
  }
  .loading {
    animation: spin 1s infinite linear;
  }
}
</style>
