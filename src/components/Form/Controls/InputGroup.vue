<template>
  <div class="fd-input-group" :class="classes">
    <span
      v-if="hasBefore"
      class="fd-input-group__addon fd-input-group__addon--before"
    >
      <slot name="before">{{ before }}</slot>
    </span>
    <slot />
    <span v-if="hasAfter" :class="afterClasses">
      <slot name="after">{{ after }}</slot>
    </span>
  </div>
</template>

<script>
export default {
  name: "FdInputGroup",
  props: {
    before: { type: String, default: null },
    after: { type: String, default: null },
    afterClass: { type: String, default: null },
    compact: { type: Boolean, default: false }
  },
  computed: {
    hasBefore() {
      return this.before != null || this.$slots.before != null;
    },
    hasAfter() {
      return this.after != null || this.$slots.after != null;
    },
    afterClasses() {
      const afterClass = this.afterClass;
      return [
        "fd-input-group__addon",
        "fd-input-group__addon--after",
        this.compact ? "fd-input-group--compact" : "",
        ...(afterClass != null ? [afterClass] : [])
      ];
    },
    classes() {
      return {
        "fd-input-group--before": this.before || this.$slots.before,
        "fd-input-group--after": this.after || this.$slots.after,
        "fd-input-group--compact": this.compact
      };
    }
  }
};
</script>
