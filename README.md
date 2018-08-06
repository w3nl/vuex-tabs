# vuex-tabs
Tabs component for Vue.js/Vuex

## Installation:

NPM:
```bash
npm install --save vuex-tabs
```
Yarn:
```bash
yarn add vuex-tabs
```

## Usage:

```html
<template>
  <tabs>
    <tab title="Tab 1" active="true">
      Tab 1 content
    </tab>
    <tab title="Tab 2">
      Tab 2 content
    </tab>
    <tab title="Tab 3">
      Tab 3 content
    </tab>
  </tabs>
</template>

<script>
import { Tabs, Tab } from 'vuex-tabs';

export default {
  components: { Tabs, Tab }
}
</script>
```
