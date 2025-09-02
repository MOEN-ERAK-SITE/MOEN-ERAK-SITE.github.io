<script setup>

</script>

<template>
<main>
    <section class="section-1">
    </section>
    <section class="section-2">
    </section>
    <section class="section-3">
    </section>
</main>

</template>

<style scoped>
main {
    --dbc: black;
    background-color: var(--dbc);
}

section {
    min-height: 150dvh;
    border: 5px solid red;
}

.section-2 {
    animation: section-change-bg 1s;
    animation-timeline: view();
    animation-delay: .5s;
}

@keyframes section-change-bg {
    to {
        background-color: red;
    }
}

</style>