<template>
  <Button @click="copyToClipboard()" :class="buttonClass" :text="text" title="Copy to clipboard" />
</template>

<script setup>
import { ref } from 'vue';
import Button from './Elements/Button.vue';

const props = defineProps({
  selection: Array,
	buttonClass: { type: String, default: 'bordered-success' }
});

const text = ref('Clipboard');

const copyToClipboard = () => {
  let data = [];
  props.selection.forEach((country) => (data = data.concat(country.found)));
  navigator.clipboard
  .writeText(JSON.stringify({ customCoordinates: data }))
  .then(() => {
    text.value = 'Copied';
    setTimeout(() => {
      text.value = 'Clipboard';
    }, 1000);
  })
  .catch((err) => {
    console.log('Something went wrong', err);
  });
};
</script>
