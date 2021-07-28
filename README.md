# vue-hinted-input
![npm](https://img.shields.io/npm/v/vue-hinted-input)

## Install
```
npm i vue-hinted-input
```

## Usage
```
<template>
  <div id="app">
    <hintedInput
        :id="'input-id'"
        :hint="'Displayed hint'"
    ></hintedInput>
  </div>
</template>

<script>
import hintedInput from 'vue-hinted-input';

export default {
  name: 'App',
  components: {
    hintedInput
  }
}
</script>

<style>
</style>
```
