<template>
  <button :class="classes" @click="click" :disabled="disabled">
    <slot />
  </button>
</template>

<script>
import ButtonTypes from "./ButtonTypes";
import { Icon, Uid } from "./../../mixins";

export default {
  name: "FdButton",
  mixins: [Icon, Uid],
  props: {
    compact: Boolean,
    styling: {
      type: String,
      default: null,
      validator: value => ["emphasized", "light"].indexOf(value) >= 0
    },
    type: {
      type: String,
      default: null,
      validator: value => ButtonTypes.indexOf(value) >= 0
    },
    state: {
      type: String,
      default: "normal",
      validator: value => ["normal", "selected", "disabled"].indexOf(value) >= 0
    }
  },
  methods: {
    click(event) {
      if (this.state === "disabled") {
        event.stopImmediatePropagation();
        return;
      }
      this.$emit("click", event);
    }
  },
  computed: {
    disabled() {
      return this.state === "disabled";
    },
    classes() {
      return [
        this.styling ? "" : "fd-button",
        this.compact ? "fd-button--compact" : "",
        this.styling ? `fd-button--${this.styling}` : "",
        this.type ? `fd-button--${this.type}` : "",
        this.state !== "normal" ? `is-${this.state}` : "",
        ...this.iconClasses
      ];
    }
  }
};
</script>
