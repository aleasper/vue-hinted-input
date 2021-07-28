<template>
  <div
      class="field-container"
      ref="wrapper"
  >
    <input
        :id="id"
        class="field-input"
        name="inputName"
        type="text"
        :placeholder="hint"

        :value="value"
        @input="handleInput"

        ref="input"
    >
    <label
        class="field-placeholder"
        :for="id"
    >{{hint}}</label>
    <div
        v-if="search"
        v-bind:class="{ 'overlay-img': true, 'search-ing': empty, 'x-img':  !empty || clearable}"
        v-on:click="clear"
    ></div>
  </div>
</template>

<script>
export default {
  name: "VueHintedInput",
  props: {
    id: {
      required: true
    },
    hint: {
      default: ''
    },
    value: {
    },
    search: {
      type: Boolean,
      default: false
    },
    clearable: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    handleInput(e) {
      this.$emit('input', e.target.value);
      this.$emit('change', e.target.value);
    },
    clear() {
      if (!this.empty) {
        this.$emit('input', '');
        this.$emit('change', '');
      }
    }
  },
  mounted() {
    this.$refs.input.onfocus = () => {
      if (!this.$refs.wrapper.classList.contains('focused')) this.$refs.wrapper.classList.add('focused');
    }
    this.$refs.input.onblur = () => {
      if (this.$refs.wrapper.classList.contains('focused')) this.$refs.wrapper.classList.remove('focused');
    }
  },
  computed: {
    empty: function() {
      return this.value != null && this.value.length === 0;
    }
  }
}
</script>

<style scoped lang="scss">
$field-container-padding: 5px;
$label-padding: $field-container-padding !default;
$border-color: #C4C4C4;
$input-hint-color: #C1C1C1;
$hint-font-weight: 400;
$main-font-weight: 400;
$accent: #009BF1;
$hover-color: #F9F9F9;

.field-container {
  position: relative;
  border: 1px solid $border-color;
  border-radius: 6px;
  height: 45px;
  min-width: 210px;
  padding-left: 12px;
  background: #FFFFFF;
  color: $input-hint-color;
  font-weight: $hint-font-weight;
  font-family: Roboto, sans-serif;

  &:active {
    border: 1px solid $accent;
  }

  &:hover:not(.focused) {
    background: $hover-color;
  }
}

.field-placeholder {
  position: absolute;

  top: 50%;
  transform: translate(#{$label-padding}, -50%);
  pointer-events: none;
  transition: all 0.14s ease-in-out;
  font-size: 18px;
  color: $input-hint-color;
  font-weight: $hint-font-weight;
}

input[type="text"].field-input {
  color: #000;
  background: transparent;
  font-weight: $main-font-weight;
  border: none;
  border-radius: 6px;
  padding: $label-padding;
  margin-top: 16px;
  font-size: 16px;
  display: block;
  box-sizing: border-box;
  width: 100%;
  bottom: 0;
  &:focus {
    outline: none;
  }
  &:focus,
  &:not(:placeholder-shown) {
    border-color: transparent;
    ~ label {
      color: $input-hint-color;
      font-weight: $hint-font-weight;
      font-size: 13px;
      top: calc(28% - 0.5rem);
      transform: translate(#{$label-padding}, 0%);
    }
  }

  &::-webkit-input-placeholder {
    color: transparent;
  }
  &::-moz-placeholder {
    color: transparent;
  }
  &:-ms-input-placeholder {
    color: transparent;
  }
}
.overlay-img {
  position: absolute;
  top: calc(50% - 12px);
  right: 10px;
  z-index: 1;
  background-repeat: no-repeat, repeat;
  background-image: url('../assets/search.svg');
  background-size: 100%;
  width: 24px;
  height: 24px;
}

.search-img {
  background-image: url('../assets/search.svg');
}

.x-img {
  top: calc(50% - 6px);
  width: 12px;
  height: 12px;
  right: 16px;
  background-image: url('../assets/close_x.svg');
}

.focused {
  border: 1px solid $accent;
}
</style>
