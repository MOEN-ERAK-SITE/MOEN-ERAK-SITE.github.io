<script setup>
import { ref } from 'vue';
import { RouterLink } from 'vue-router';

const isOpen = ref(false);

</script>

<template>
  <section class="nav-menu position-fixed top-0 start-0 overflow-hidden" :class="{ 'open': isOpen }" ref="navMenu">
    <button class="btn-menu rounded-circle position-absolute p-3" :class="{ 'active': isOpen }"
      @click="isOpen = !isOpen" ref="btnMenu">
      <div class="burger"></div>
    </button>
    <div class="wrapper position-absolute top-0 left-0 w-100 h-100">
      <h1 class="text-light">Another thing</h1>
      <ul class="menu-list list-unstyled">
        <li @click="isOpen = !isOpen">
          <RouterLink to="/" class="menu-link" :class="{ 'active': $route.path === '/' }">
            <div class="nav-arrow">
            </div>
            <span>Home</span>
          </RouterLink>
        </li>
        <li @click="isOpen = !isOpen">
          <RouterLink to="/myself" class="menu-link" :class="{ 'active': $route.path === '/myself' }">
            <div class="nav-arrow">
            </div>
            <span>Myself</span>
          </RouterLink>
        </li>
        <li>
          <RouterLink to="/" class="menu-link" :class="{ 'active': $route.path === '' }">
            <div class="nav-arrow">
            </div>
            <span>About</span>
          </RouterLink>
        </li>
        <li>
          <RouterLink to="/" class="menu-link" :class="{ 'active': $route.path === '' }">
            <div class="nav-arrow">
            </div>
            <span>Contact</span>
          </RouterLink>
        </li>
      </ul>
      <h2 class="text-light">Another thing</h2>
    </div>
  </section>
</template>

<style scoped>
section.nav-menu {
  --menu-border-gap: clamp(50px, 10dvw, 100px);

  z-index: 999;
  transition: .3s;
  width: 100%;
  height: 100dvh;

  &,
  * {
    pointer-events: none;
  }


  button.btn-menu {
    --gap: 250%;
    background-color: black;
    z-index: 9999;
    aspect-ratio: 1/1;
    border: none;
    top: 0;
    right: 0;
    transform: translate(50%, -50%);
    margin: var(--menu-border-gap);
    pointer-events: all;

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

  .wrapper {
    background-color: black;
    mask-image: radial-gradient(circle at calc(100dvw - var(--menu-border-gap)) calc(0dvh + var(--menu-border-gap)), black 2%, transparent 0%);
    mask-size: 100%;
    transition: .5s cubic-bezier(1, 0, 0, 1);
    pointer-events: none;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    --left-gap: clamp(10px, 20dvw, 200px);


    ul.menu-list {
      display: flex;
      flex-direction: column;
      row-gap: 1rem;

      li {
        .menu-link {
          color: whitesmoke;
          font-size: var(--font-size-3xl);
          text-decoration: none;
          font-weight: bolder;
          letter-spacing: .2rem;
          line-height: 100%;
          display: flex;
          /* border: 1px solid red; */
          column-gap: 2rem;
          & , * {
            transition: .3s;
          }


          .nav-arrow {
            width: var(--left-gap);
            min-height: 100%;
          }

          &.active {
            .nav-arrow {
              background-color: greenyellow;
            }
          }
        }
      }
    }
  }

  &.open {

    &,
    * {
      pointer-events: all;
    }


    .wrapper {
      mask-size: 20000%;
    }
  }
}
</style>
