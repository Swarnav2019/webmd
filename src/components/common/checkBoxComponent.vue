<template>
    <v-checkbox
        v-model="checkFieldValue"
        :label="label"
        color="#fb8c00"
        required
        >
    </v-checkbox>
</template>

<script>
export default {
  name: 'checkBoxComponent',
  props: {
      value: Boolean,
      label: String,
    },
  data() {
      return {
          checkFieldValue: true,
      }
  },
  watch: {
    value: {
      immediate: true,
      handler(v) {
          this.checkFieldValue = v;
      }
    }
  },
}
</script>