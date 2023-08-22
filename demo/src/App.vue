<script setup lang="ts">
import { ref, watch, nextTick } from 'vue';
import VueTurnstile from '../../src';

const cfTurnstileToken = ref<string>('');
const cfTurnstile = ref<typeof VueTurnstile>();

const siteKey = ref<string>('1x00000000000000000000AA')
// Default = 4.5 mins
const resetIntervalMs = ref<number>(60 * 4.5 * 1000);

const sizeOptions = ['normal', 'compact'];
const size = ref<'normal' | 'compact'>('normal');

const themeOptions = ['auto', 'light', 'dark'];
const theme = ref<'light' | 'dark' | 'auto'>('auto');

const displayTurnstile = ref<boolean>(true);

const action = ref<string>('');
const removeBeforeUnmount = ref<boolean>(true);

function firstCapital(str: string) {
  return str.charAt(0).toUpperCase() + str.slice(1);
}

watch([siteKey, resetIntervalMs, size, theme, action], async () => {
  nextTick(() => {
    cfTurnstile.value?.remove();
    // Function defined by vue-turnstile component
    cfTurnstile.value?.render!();
  });
});
</script>

<template>
  <div class="col-lg-8 mx-auto p-4 py-md-5">
    <header class="d-flex align-items-center pb-3 mb-5 border-bottom">
      <a href="/" class="d-flex align-items-center text-body-emphasis text-decoration-none">
        <span class="fs-4">Turnstile Demo</span>
      </a>
    </header>

    <main>

      <div class="row g-5">
        <div class="col-md-6">
          <h2 class="text-body-emphasis">Options</h2>
          <ul class="list-unstyled ps-0">
            <li>
              <div class="mb-3">
                <button type="button" class="btn btn-primary" @click.prevent="displayTurnstile = !displayTurnstile">{{
                  displayTurnstile ? 'Hide turnstile' : 'Show turnstile' }}</button>
              </div>
            </li>
            <li>
              <div class="mb-3">
                <label for="siteKeyInput" class="form-label">Site Key</label>
                <input class="form-control" id="siteKeyInput" v-model="siteKey">
              </div>
            </li>
            <li>
              <div class="mb-3">
                <label for="actionInput" class="form-label">Action</label>
                <input class="form-control" id="actionInput" v-model="action">
              </div>
            </li>

            <li>
              <div class="mb-3">
                <label for="resetIntervalInput" class="form-label">Reset interval (ms)</label>
                <input type="number" class="form-control" id="resetIntervalInput" v-model="resetIntervalMs">
              </div>
            </li>
            <li>
              <div class="form-check">
                <input class="form-check-input" type="checkbox" name="remove-before-unmount" id="remove-before-unmount"
                  v-model="removeBeforeUnmount">
                <label class="form-check-label" for="remove-before-unmount">
                  Remove before unmount
                </label>
              </div>
            </li>
            <li>
              <div>Size</div>


              <div class="form-check" v-for="sizeOption in sizeOptions">
                <input class="form-check-input" type="radio" name="size" :value="sizeOption" :id="`size-${sizeOption}`"
                  v-model="size">
                <label class="form-check-label" :for="`size-${sizeOption}`">
                  {{ firstCapital(sizeOption) }}
                </label>
              </div>

            </li>
            <li>
              <div>Theme</div>

              <div class="form-check" v-for="themeOption in themeOptions">
                <input class="form-check-input" type="radio" name="theme" :value="themeOption"
                  :id="`theme-${themeOption}`" v-model="theme">
                <label class="form-check-label" :for="`theme-${themeOption}`">
                  {{ firstCapital(themeOption) }}
                </label>
              </div>
            </li>

            <hr>

            <li>
              <input class="form-control" id="cfTurnstileToken" v-model="cfTurnstileToken" readonly>
            </li>
          </ul>
        </div>
        <div class="col-md-6">
          <h2 class="text-body-emphasis">Component</h2>
          <vue-turnstile v-if="displayTurnstile" ref="cfTurnstile" v-model="cfTurnstileToken" :theme="theme"
            :site-key="siteKey" :size="size" :action="action" :reset-interval="resetIntervalMs" />
        </div>


      </div>
    </main>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
