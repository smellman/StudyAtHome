<template>
  <v-text-field
    v-if="type === 'password'"
    :value="value"
    :color="textFieldColor"
    :type="show ? 'text' : 'password'"
    :hint="hint"
    :label="label"
    :placeholder="placeholder"
    background-color="white"
    class="elevation-0"
    solo
    flat
    outlined
    @input="$emit('input', $event)"
  >
    <template v-slot:prepend-inner>
      <v-icon :color="prependIconColor">{{ prependIcon }}</v-icon>
    </template>
    <template v-slot:append>
      <v-icon
        color="blue"
        @click="show = !show"
        v-text="show ? 'mdi-eye' : 'mdi-eye-off'"
      />
    </template>
  </v-text-field>
  <v-text-field
    v-else-if="type === 'email'"
    :value="value"
    :color="textFieldColor"
    type="text"
    :hint="hint"
    :label="label"
    :placeholder="placeholder"
    background-color="white"
    class="elevation-0"
    solo
    flat
    outlined
    @input="$emit('input', $event)"
  >
    <template v-slot:prepend-inner>
      <v-icon :color="prependIconColor">{{ prependIcon }}</v-icon>
    </template>
  </v-text-field>
  <v-text-field
    v-else-if="type === 'classId'"
    :value="value"
    :color="textFieldColor"
    type="text"
    :hint="hint"
    :label="label"
    :placeholder="placeholder"
    background-color="white"
    class="elevation-0"
    solo
    flat
    outlined
    @input="$emit('input', $event)"
  >
    <template v-slot:prepend-inner>
      <v-icon :color="prependIconColor">{{ prependIcon }}</v-icon>
    </template>
  </v-text-field>
  <v-text-field
    v-else
    :value="value"
    :color="textFieldColor"
    type="text"
    :hint="hint"
    :label="label"
    :placeholder="placeholder"
    background-color="white"
    class="elevation-0"
    solo
    flat
    outlined
    @input="$emit('input', $event)"
  >
    <template v-slot:prepend-inner>
      <v-icon :color="prependIconColor">{{ prependIcon }}</v-icon>
    </template>
  </v-text-field>
</template>

<script lang="ts">
import Vue from 'vue'
type DataType = {
  show: boolean
}
export default Vue.extend({
  name: 'BaseInputField',
  props: {
    value: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      required: false,
      default: 'text',
    },
    label: {
      type: String,
      required: true,
      default: '',
    },
    hint: {
      type: String,
      required: false,
      default: '',
    },
    appendIcon: {
      type: String,
      required: false,
      default: '',
    },
    require: {
      type: Boolean,
      required: false,
      default: false,
    },
    placeholder: {
      type: String,
      required: false,
      default: '',
    },
  },
  data(): DataType {
    return {
      show: false,
    }
  },
  computed: {
    prependIconColor(): string {
      const classIdPattern = /^[あ-ん]{6}$/
      if (this.type === 'classId') {
        if (!this.value || !classIdPattern.test(this.value)) return '#C01B61'
      }
      if (this.type === 'email') {
        if (
          !this.value ||
          !this.value.match(/^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/)
        )
          return '#C01B61'
      }
      if (this.require) {
        if (!this.value) return '#C01B61'
      }
      if (this.value) {
        return '#138945'
      }
      return '#BDBDBD'
    },
    textFieldColor(): string {
      const classIdPattern = /^[あ-ん]{6}$/
      if (this.type === 'classId') {
        if (!this.value || !classIdPattern.test(this.value)) return '#C01B61'
      }
      if (this.type === 'email') {
        if (
          !this.value ||
          !this.value.match(/^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/)
        )
          return '#C01B61'
      }
      if (this.require) {
        if (!this.value) return '#C01B61'
      }
      return '#0071C2'
    },
    prependIcon(): string {
      const classIdPattern = /^[あ-ん]{6}$/
      if (this.type === 'classId') {
        if (!this.value || !classIdPattern.test(this.value))
          return 'mdi-alert-circle'
      }
      if (this.type === 'email') {
        if (
          !this.value ||
          !this.value.match(/^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/)
        )
          return 'mdi-alert-circle'
      }
      if (this.require) {
        if (!this.value) return 'mdi-alert-circle'
      }
      return 'mdi-check-circle'
    },
  },
})
</script>

<style scoped lang="scss">
.v-text-field > .v-input__control > .v-input__slot {
  box-shadow: inset 2px 2px 5px rgba(0, 0, 0, 0.3);
  border-radius: 14px !important;
}
</style>
