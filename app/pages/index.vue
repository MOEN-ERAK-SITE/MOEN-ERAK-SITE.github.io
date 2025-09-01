<script setup>
import { onMounted, ref } from 'vue'
import { Icon } from '@iconify/vue'
const textSlider = ref(null)
const mouseShow = ref(null)

let setIntervalId = null

function onChangeSet(currentSet = 1) {
    const textSliderElement = textSlider.value
    if (!textSliderElement) return
    textSliderElement.classList.forEach(cls => {
        if (cls.startsWith('set-')) {
            textSliderElement.classList.remove(cls)
        }
    })
    if (setIntervalId) {
        clearInterval(setIntervalId)
        setIntervalId = null
    }
    textSliderElement.classList.add(`set-${currentSet}`)
    const changeSet = () => {
        textSliderElement.classList.forEach(cls => {
            if (cls.startsWith('set-')) {
                textSliderElement.classList.remove(cls)
            }
        })
        currentSet = currentSet < 4 ? currentSet + 1 : 1
        textSliderElement.classList.add(`set-${currentSet}`)
    }
    setIntervalId = setInterval(changeSet, 3000)
}


onMounted(() => {

    onChangeSet()

    var subtitle = document.querySelector('.subtitle[role*="button"]');
    subtitle.classList.add('hover')
    setTimeout(() => {
        subtitle.classList.remove('hover')
    }, 2000);

    const handleMouseMove = (e) => {
        if (!mouseShow.value) return
        const x = e.clientX
        const y = e.clientY
        mouseShow.value.style.maskImage = `radial-gradient(circle at ${x}px ${y}px, black 5dvw, transparent 30dvw)`
    }
    window.addEventListener('mousemove', handleMouseMove)
    // Clean up
    onBeforeUnmount(() => {
        window.removeEventListener('mousemove', handleMouseMove)
    })
})

</script>


<template>
    <section class="hero-banner position-relative">
        <div id="mouse-show" ref="mouseShow"></div>
        <div class="container-fluid h-100 d-flex flex-column justify-content-center py-3">
            <h3 class="subtitle position-absolute top-0 start-0 btn" style="margin: 5dvw;" role="button"
                @click="onChangeSet(2)">
                <span>What I</span> <span class="non-job">can</span><span>do</span>
                <Icon icon="proicons:arrow-enter" width="24" height="24" style="transform: rotate(-90deg);" />
            </h3>
            <div class="text-slider" id="text_slider" ref="textSlider">
                <div class="wrapper">
                    <div class="vertical-text-wrapper">
                        <span id="anchorSubtitle">H</span>
                        <span>P</span>
                        <span>E</span>
                        <span>W</span>
                        <span>A</span>
                        <span>R</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>B</span>
                        <span>N</span>
                        <span>R</span>
                        <span>N</span>
                        <span>E</span>
                        <span>W</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>G</span>
                        <span>B</span>
                        <span>G</span>
                        <span>O</span>
                        <span>A</span>
                        <span>R</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>R</span>
                        <span>D</span>
                        <span>G</span>
                        <span>I</span>
                        <span>L</span>
                        <span>T</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>H</span>
                        <span>Y</span>
                        <span>N</span>
                        <span>R</span>
                        <span>E</span>
                        <span>O</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>M</span>
                        <span>V</span>
                        <span>A</span>
                        <span>E</span>
                        <span>Z</span>
                        <span>O</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>S</span>
                        <span>O</span>
                        <span>E</span>
                        <span>M</span>
                        <span>E</span>
                        <span>N</span>
                    </div>
                    <div class="vertical-text-wrapper">
                        <span>R</span>
                        <span>P</span>
                        <span>S</span>
                        <span>R</span>
                        <span>R</span>
                        <span>O</span>
                    </div>
                </div>
                <div class="hidden-wrapper">
                    <span class="hidden">ABCDEFGR</span>
                    <span class="hidden">ABCDEFGR</span>
                    <span class="hidden">ABCDEFGR</span>
                </div>
            </div>
            <div class="row mt-auto">
                <div class="col-6">
                    <h5>Hi, My name is MOEN ERAK Engineering student at RUPP 4th Years</h5>
                </div>
            </div>
        </div>
        <!-- <div class="wivy-arrow-wrapper position-absolute end-0 bottom-0">
            <img src="~/assets/images/ui/wivy-arrow.svg"></img>
        </div> -->
    </section>
</template>

<style scoped>
section.hero-banner {
    height: 100dvh;
    display: flex;
    flex-direction: column;
    align-items: start;
    position: relative;
    background-size: 10% 20%;
    overflow: hidden;
    isolation: isolate;
    background-color: var(--bs-dark);

    .subtitle {
        margin-bottom: -3dvw;
        position: relative;
        z-index: 1;
        font-size: var(--font-size-xl);
        font-weight: 700;
        color: var(--bs-light);

        &:hover,
        &.hover {
            background-color: greenyellow;
            color: black;
            backdrop-filter: blur(5px);
            border-radius: 0;

            .non-job {
                width: calc(var(--font-size-xl) * 2) !important;
            }

            &::before {
                content: 'Switch ';
            }

            &::after {
                content: 'And what I do';
            }
        }
    }

    .non-job {
        display: inline-flex;
        overflow: hidden;
        width: calc(var(--font-size-xl) * 2);
        transition: .2s;
    }

    &:has(.text-slider.set-2) {
        .non-job {
            width: 0;
        }
    }

    .text-slider {
        --unshow: rgb(172, 172, 172);
        --show: greenyellow;
        --number-of-line: 6;

        width: fit-content;
        min-height: fit-content;
        position: relative;
        display: flex;
        isolation: isolate;
        mask-image: linear-gradient(to bottom, transparent 20%, hsl(from black h s l / .2), black 35%, black 65%, hsl(from black h s l / .2), transparent 80%);
        overflow: hidden;

        span {
            font-size: 22.6dvw;
            font-weight: 900;
            line-height: .75;
            color: var(--unshow);
            font-family: monospace;
            transition: transform 1s, color 1s;
            letter-spacing: -0.2rem;

            &:hover {
                font-style: italic;
            }
        }

        .wrapper {
            display: flex;
            position: absolute;
            z-index: -1;
            width: 100%;
            height: fit-content;
            /* opacity: 0; */

            .vertical-text-wrapper {
                display: flex;
                flex-direction: column;
                position: relative;
                transition: 1s ease-in-out;
                transform: translateY(calc(-100% / var(--number-of-line) * 1));

                span {
                    text-align: center;
                }
            }
        }

        .hidden-wrapper {
            display: flex;
            flex-direction: column;
            position: relative;
            pointer-events: none;

            .hidden {
                opacity: 0;
            }
        }

        &.set-1 {
            .wrapper {
                .vertical-text-wrapper:nth-child(1) {
                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(2) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(3) {
                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(4) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(5) {

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(6) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(7) {

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(8) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }
            }
        }

        &.set-2 {
            .wrapper {
                .vertical-text-wrapper:nth-child(1) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(2) {
                    transform: translateY(-50%);

                    span:nth-child(5) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(3) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(4) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(5) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 3));

                    span:nth-child(5) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(6) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(7) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(8) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }
            }
        }

        &.set-3 {
            .wrapper {
                .vertical-text-wrapper:nth-child(1) {
                    transform: translateY(calc(100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(2) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 1));

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(3) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(4) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 1));

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(5) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(6) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 1));

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(7) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(8) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 1));

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }
            }
        }

        &.set-4 {
            .wrapper {
                .vertical-text-wrapper:nth-child(1) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 3));

                    span:nth-child(5) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(2) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(3) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 3));

                    span:nth-child(5) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(4) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 3));

                    span:nth-child(5) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(5) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 0));

                    span:nth-child(2) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(6) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 3));

                    span:nth-child(5) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(7) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 1));

                    span:nth-child(3) {
                        color: var(--show);
                    }
                }

                .vertical-text-wrapper:nth-child(8) {
                    transform: translateY(calc(-100% / var(--number-of-line) * 2));

                    span:nth-child(4) {
                        color: var(--show);
                    }
                }
            }
        }
    }

    div#mouse-show {
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
        background-size: 10dvw 10dvw;
        background-image: linear-gradient(to right, green 1px, transparent 1px), linear-gradient(to bottom, green 1px, transparent 1px);
        mask-image: radial-gradient(circle at center, transparent 100%);
        transition: .3s;
        z-index: -1;
    }

    .wivy-arrow-wrapper {
        --bg-color: var(--bs-secondary);
        --animation-move-scale: 10px;
        width: clamp(150px, 40dvw, 500px);
        background-color: var(--bg-color);
        mask-image: url('~/assets/images/ui/wivy-arrow.svg');
        mask-size: 100% 100%;
        animation: wivy-arrow-move 3s infinite ease-in-out alternate;

        img {
            width: 100%;
            opacity: 0;
        }
    }
}

@keyframes wivy-arrow-move {
    0% {
        transform: translate(var(--animation-move-scale), var(--animation-move-scale));
    }

    25% {
        transform: translate(calc(-1 * var(--animation-move-scale)), calc(-1 * var(--animation-move-scale)));
    }

    50% {
        transform: translate(calc(-1 * var(--animation-move-scale)), var(--animation-move-scale));
    }

    75% {
        transform: translate(var(--animation-move-scale), calc(-1 * var(--animation-move-scale)));
    }

    100% {
        transform: translate(var(--animation-move-scale), var(--animation-move-scale));
    }
}
</style>