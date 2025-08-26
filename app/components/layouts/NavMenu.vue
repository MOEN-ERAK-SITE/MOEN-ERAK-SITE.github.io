<script setup>
import { ref, watch, onBeforeUnmount } from 'vue';

const isOpen = ref(false);
const btnMenu = ref(null);
const wrapper = ref(null);
const navList = ref(null);

let animFrameId = null;

// Position navList relative to wrapper
function updateNavListPosition() {
  if (!wrapper.value || !navList.value) return;

  const rect = wrapper.value.getBoundingClientRect();
  navList.value.style.transform = `translate(${-rect.x}px, ${-rect.y}px)`;
}

// Keep wrapper centered on button
function updateWrapperPosition() {
  if (!wrapper.value || !btnMenu.value) return;

  const btnRect = btnMenu.value.getBoundingClientRect();
  const wrapperRect = wrapper.value.getBoundingClientRect();

  const btnCenterX = btnRect.left + btnRect.width / 2;
  const btnCenterY = btnRect.top + btnRect.height / 2;

  const left = btnCenterX - wrapperRect.width / 2;
  const top = btnCenterY - wrapperRect.height / 2;

  wrapper.value.style.left = `${left}px`;
  wrapper.value.style.top = `${top}px`;
}

// Animate positions each frame
function animate() {
  updateWrapperPosition();
  updateNavListPosition();
  animFrameId = requestAnimationFrame(animate);
}

// Watch open/close
watch(isOpen, () => {
  if (!animFrameId) animate();

  // Stop animation after transition duration
  setTimeout(() => {
    if (animFrameId) {
      cancelAnimationFrame(animFrameId);
      animFrameId = null;
      updateWrapperPosition();
      updateNavListPosition();
    }
  }, 500); // adjust to your CSS transition
});

onBeforeUnmount(() => {
  if (animFrameId) cancelAnimationFrame(animFrameId);
});
</script>

<template>
  <button 
    class="btn-menu rounded-circle position-absolute end-0 top-0 m-5 p-3" 
    :class="{ 'active': isOpen }"
    @click="isOpen = !isOpen" 
    ref="btnMenu"
  >
    <div class="burger"></div>
  </button>

  <section class="nav-menu position-fixed top-0 start-0" :class="{ 'open': isOpen }" ref="navMenu">
    <div class="wrapper position-absolute" ref="wrapper">
      <ul class="nav-list list-unstyled display-1 text-light" ref="navList">
        <li><button>Placeholder</button></li>
        <li><button>Placeholder</button></li>
        <li><button>Placeholder</button></li>
        <li><button>Placeholder</button></li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
button.btn-menu {
  --gap: 250%;
  z-index: 9999;
  aspect-ratio: 1/1;
  background: black;
  border: none;

  .burger {
    width: 3rem;
    height: 0.3rem;
    position: relative;

    &,
    &::before,
    &::after {
      background-color: white;
      border-radius: 100vmax;
      transition: 0.3s;
    }

    &::before,
    &::after {
      content: '';
      position: absolute;
      width: 80%;
      height: 100%;
      right: 0%;
    }

    &::before {
      transform: translateY(calc(var(--gap) * -1));
    }

    &::after {
      transform: translateY(var(--gap));
    }
  }

  &.active {
    --gap: 0%;

    .burger {
      background: transparent;

      &::before,
      &::after {
        background-color: white;
        width: 100%;
      }

      &::before {
        transform: translateY(calc(var(--gap) * -1)) rotate(45deg);
      }

      &::after {
        transform: translateY(var(--gap)) rotate(-45deg);
      }
    }
  }
}

section.nav-menu {
  pointer-events: none;
  z-index: 999;
  transition: 0.3s;
  width: 100%;
  height: 100dvh;

  .wrapper {
    width: 0;
    aspect-ratio: 1/1;
    background-color: black;
    border-radius: 100%;
    transition: width 0.5s , height 0.5s;
    overflow: hidden;

    .nav-list {
      position: absolute;
      width: 100dvw;
      height: 100dvh;
    }
  }

  &.open {
    pointer-events: all;
    .wrapper {
      width: 300dvw;
      .nav-list {
        opacity: 1;
      }
    }
  }
}
</style>
