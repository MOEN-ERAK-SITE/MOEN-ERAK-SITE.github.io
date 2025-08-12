<script setup>
import { onMounted, ref } from 'vue'
const textSlider = ref(null)
const mouseShow = ref(null)

onMounted(() => {
    const textSliderElement = textSlider.value
    let currentSet = 1
    textSliderElement.classList.add(`set-${currentSet}`)
    const changeSet = () => {
        textSliderElement.classList.remove(`set-${currentSet}`)
        currentSet = currentSet < 4 ? currentSet + 1 : 1
        textSliderElement.classList.add(`set-${currentSet}`)
    }
    setInterval(changeSet, 5000)

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
    <section class="hero-banner">
        <div id="mouse-show" ref="mouseShow"></div>
        <div class="container h-100 d-flex flex-column justify-content-center py-3">
            <h1 class="subtitle">What I do</h1>
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
                    <span class="hidden">AAAAAAAAAAA</span>
                    <span class="hidden">AAAAAAAAAAA</span>
                    <span class="hidden">AAAAAAAAAAA</span>
                </div>
            </div>
            <div class="row mt-auto">
                <div class="col-6">
                    <h5>Hi, My name is MOEN ERAK Engineering student at RUPP 4th Years</h5>
                </div>
            </div>
        </div>
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

    .subtitle {
        margin-bottom: -5rem;
        position: relative;
        z-index: 1;
        width: fit-content;
    }

    .text-slider {
        --unshow: rgb(172, 172, 172);
        --show: black;
        --number-of-line: 6;

        width: fit-content;
        position: relative;
        display: flex;
        isolation: isolate;
        mask-image: linear-gradient(to bottom, transparent 10%, red 50%, transparent 90%);
        overflow: hidden;

        span {
            font-size: 10dvw;
            line-height: 90%;
            color: var(--unshow);
            font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
            transition: 1s;
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
        background-size: 10% 20%;
        background-image: linear-gradient(to right, green 1px, transparent 1px), linear-gradient(to bottom, green 1px, transparent 1px);
        mask-image: radial-gradient(circle at center, transparent 100%);
        transition: .3s;
        z-index: -1;
    }
}
</style>