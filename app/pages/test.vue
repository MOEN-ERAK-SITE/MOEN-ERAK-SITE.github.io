
<script setup>
import { ref } from 'vue';

const font5xl = ref(null)
const font4xl = ref(null)
const font3xl = ref(null)
const font2xl = ref(null)
const fontXl = ref(null)
const fontMd = ref(null)
const fontBase = ref(null)
const fontSm = ref(null)

const fontSize5xl = ref(null)
const fontSize4xl = ref(null)
const fontSize3xl = ref(null)
const fontSize2xl = ref(null)
const fontSizeXl = ref(null)
const fontSizeMd = ref(null)
const fontSizeBase = ref(null)
const fontSizeSm = ref(null)

window.addEventListener('resize', () => {
  const fontRefs = [
    { ref: font5xl, sizeRef: fontSize5xl },
    { ref: font4xl, sizeRef: fontSize4xl },
    { ref: font3xl, sizeRef: fontSize3xl },
    { ref: font2xl, sizeRef: fontSize2xl },
    { ref: fontXl,  sizeRef: fontSizeXl },
    { ref: fontMd,  sizeRef: fontSizeMd },
    { ref: fontBase, sizeRef: fontSizeBase },
    { ref: fontSm,  sizeRef: fontSizeSm }
  ];

  fontRefs.forEach(({ ref, sizeRef }) => {
    if (ref && ref.value) {
      const size = window.getComputedStyle(ref.value).fontSize;
      if (size && size.endsWith('px')) {
        const num = parseFloat(size);
        sizeRef.value = `${num.toFixed(2)}px`;
      } else {
        sizeRef.value = size;
      }
    }
  });
})



</script>

<template>

<section class="wrapper d-flex flex-column">

  <span class="font-size-5xl" ref="font5xl">Font 5xl ({{ fontSize5xl }})</span>
  <span class="font-size-4xl" ref="font4xl">Font 4xl ({{ fontSize4xl }})</span>
  <span class="font-size-3xl" ref="font3xl">Font 3xl ({{ fontSize3xl }})</span>
  <span class="font-size-2xl" ref="font2xl">Font 2xl ({{ fontSize2xl }})</span>
  <span class="font-size-xl" ref="fontXl">Font xl ({{ fontSizeXl }})</span>
  <span class="font-size-md" ref="fontMd">Font md ({{ fontSizeMd }})</span>
  <span class="font-size-base" ref="fontBase">Font base ({{ fontSizeBase }})</span>
  <span class="font-size-sm" ref="fontSm">Font sm ({{ fontSizeSm }})</span>
</section>

</template>

<style scoped>
.wrapper {
  overflow-anchor: hidden;
}
span {
  white-space: nowrap;
}
</style>