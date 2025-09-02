<script setup>
import { onMounted, reactive } from 'vue';
import hero from '~/components/sections/index/hero.vue';

const sectionState = reactive({
    randomPhotos: {
        el: null,
        isIntersect: false,
        option: {
            threshold: 0.3
        },
        observer: null
    }
})

onMounted(() => {
    sectionState.randomPhotos.el = document.querySelector('section.random-photos');

    for (const key in sectionState) {
        const section = sectionState[key];
        if (!section.el) continue;
        section.observer = new IntersectionObserver((entries) => {
            entries.forEach((entry) => {
                section.isIntersect = entry.isIntersecting
            })
        },
            section.option
        )
        section.observer.observe(section.el)
    }
})

onUnmounted(() => {
    for (const key in sectionState) {
        const section = sectionState[key];
        if (!section.el || !section.observer) continue;
        section.observer.unobserve(section.el)
    }
})

</script>


<template>
    <main :class="{ 'random-photo-entering': sectionState.randomPhotos.isIntersect }">
        <hero />
        <section class="random-photos">
        </section>
    </main>
</template>

<style scoped>
main {
    transition: background-color 1s;

    background-color: var(--color-secondary);

    &.random-photo-entering {
        background-color: var(--color-background);
    }
}

section.random-photos {
    min-height: 150dvh;
}
</style>