<template>
  <span class="no-wrap">{{displayValue}}</span>
</template>

<script>
import mixin from "../../../mixins/interface";

export default {
  mixins: [mixin],
  computed: {
    displayValue() {
      let value = this.value;

      if (value) {
        const choices =
          typeof this.options.choices === "string"
            ? JSON.parse(this.options.choices)
            : this.options.choices;

        if (this.options.wrapWithDelimiter) {
          value = value.slice(1, -1);
        }

        value = value.split(",");

        value = value
          .map(val => {
            if (this.options.formatting === "text") {
              return choices[val];
            }

            return val;
          })
          .join(", ");
      }

      return value;
    }
  }
};
</script>
