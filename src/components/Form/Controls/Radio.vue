<template>
  <input
    type="radio"
    class="fd-form__control"
    :class="inputClasses"
    :id="inputId"
    :disabled="disabled ? '' : null"
    :checked="checked ? true : false"
    :value="value"
    @input="$emit('update', $event.target.value, $event)"
    v-on="$listeners"
    v-bind="$attrs"
  />
</template>

<script>
import InputMixin from "./InputMixin";
import { $valueWithDefault, $modelValueWithDefault } from "./Helper/prop";

export default {
  name: "FdRadio",
  mixins: [InputMixin],
  inheritAttrs: false,
  model: {
    prop: "modelValue",
    event: "update"
  },
  inject: {
    // We need the form item so that we can say tell the form item
    // to render the checked-style
    formItem: { default: null }
  },
  props: {
    value: $valueWithDefault(false),
    modelValue: $modelValueWithDefault(false)
  },
  mounted() {
    const formItem = this.formItem;
    if (formItem) {
      formItem.setCheck(true);
    }
  },
  computed: {
    checked() {
      return this.modelValue === this.value;
    }
  }
};
</script>
