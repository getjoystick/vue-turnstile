# vue-turnstile

[![Latest Stable Version](https://img.shields.io/npm/v/@getjoystick/vue-turnstile)](https://www.npmjs.com/package/@getjoystick/vue-turnstile)

A [Cloudflare Turnstile](https://developers.cloudflare.com/turnstile/) library for Vue 3

## Installation

Add `vue-turnstile` to your Javascript project dependencies using Yarn:

```bash
yarn add vue-turnstile
```

Or NPM:

```bash
npm install vue-turnstile --save
```

## Usage

```vue
<script lang="ts">
import VueTurnstile from 'vue-turnstile';

export default {
  components: { VueTurnstile },

  data() {
    return {
      token: '',
    };
  },
};
</script>

<template>
  <div>
    <vue-turnstile site-key="1x00000000000000000000AA" v-model="token" />
    <div>Token: {{ token }}</div>
  </div>
</template>
```

## Customization options

| Prop                  | Type                          | Description                                                                                                                           | Required | Default    |
| --------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| site-key              | `String`                      | Your Turnstile sitekey - [Docs](https://developers.cloudflare.com/turnstile/get-started/)                                             | Yes      | N/A        |
| v-model               | `String`                      | Binding that contains the token returned by the Turnstile widget                                                                      | Yes      | N/A        |
| reset-interval        | `Number`                      | Get a fresh token after `reset-interval` milliseconds - Turnstile tokens only last for 5 minutes                                      | No       | `295000`   |
| size                  | `'normal' \| 'compact'`       | Widget size                                                                                                                           | No       | `'normal'` |
| theme                 | `'light' \| 'dark' \| 'auto'` | Widget theme - auto respects the user's browser preference                                                                            | No       | `'auto'`   |
| action                | `String`                      | A customer value that can be used to differentiate widgets under the same sitekey in analytics and which is returned upon validation. | No       | `''`       |
| render-on-mount       | `Boolean`                     | Automatically render Turnstile widget after component mounts                                                                          | No       | `true`     |
| remove-before-unmount | `Boolean`                     | Automatically remove the Turnstile widget in beforeUnmount                                                                            | No       | `true`     |

## Methods

| Method     | Description        |
| ---------- | ------------------ |
| `reset()`  | Resets the widget  |
| `render()` | Renders the widget |
| `remove()` | Removes the widget |

## Author

Original author of the library is:
Rui Gomes  
https://ruigomes.me

Fork is maintained and published by:
Joystick
https://getjoystick.com

## License

The MIT License (MIT). Please see [LICENSE file](https://github.com/getjoystick/vue-turnstile/blob/main/LICENSE.md) for more information.
