<template>
    <v-text-field
        v-model="textFieldValue"
        :rules="rules"
        :prepend-inner-icon="icon"
        color="#fb8c00"
        single-line
        outlined
        required
        :type="type"
        :label="label">
    </v-text-field>
</template>

<script>
export default {
  name: 'textBoxComponent',
  props: {
      rules: {
        type: Array,
        default: []
      },
      name: {
          type: String,
          default: '',
          required: true
      },
      type: {
          type: String,
          default: 'text',
          required: true
      },
      icon: String,
      value: String,
      label: String,
    },
  data() {
      return {
          textFieldValue: '',
      }
  },
  watch: {
    textFieldValue: {
      immediate: true,
      handler(v) {
          const formData = {};
          formData[this.name] = v;
          this.$emit('update-data', formData);
      }
    }
  },
}
</script>