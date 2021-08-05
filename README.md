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
        <hinted-input
                :id="'input-id0'"
                :hint="'I am hint'"
                v-model="value0"
        ></hinted-input>
        <hinted-input
                :id="'input-id1'"
                :hint="'I am disabled'"
                :disabled="true"
                v-model="value1"
        ></hinted-input>
        <hinted-input
                :id="'input-id2'"
                :hint="'Type here for search'"
                :search="true"
                v-model="value2"
        ></hinted-input>
        <hinted-input
                :id="'input-id3'"
                :hint="'I am clearable'"
                :clearable="true"
                v-model="value3"
        ></hinted-input>
  </div>
</template>

<script>
import hintedInput from 'vue-hinted-input';

export default {
  name: 'App',
  components: {
    'hinted-input': hintedInput
  },
  data: {
    value0: '',
    value1: '',
    value2: '',
    value3: ''
  },
}
</script>

<style>
</style>
```
