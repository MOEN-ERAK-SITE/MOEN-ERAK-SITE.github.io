<script setup>
import { ref } from 'vue';
import { RouterLink } from 'vue-router';
import { Icon } from '@iconify/vue';

const isOpen = ref(true);

</script>

<template>
  <section class="nav-menu position-fixed top-0 start-0 overflow-hidden" :class="{ 'open': isOpen }" ref="navMenu">
    <button class="btn-menu rounded-circle position-absolute" :class="{ 'active': isOpen }" @click="isOpen = !isOpen"
      ref="btnMenu">
      <div class="burger"></div>
      <!-- <div class="something-wrapper">
        <div class="me-photo">
          <img src="~/assets/images/photos/me_avatar.jpeg" alt="pic" class="me-pic"></img>
        </div>
        <span class="text-dark welcome-text" style="background-color: greenyellow;"></span>
      </div> -->
    </button>
    <div class="wrapper container-fluid position-absolute top-0 left-0 w-100 h-100">
      <div class="d-flex justify-content-between flex-column flex-md-row">
        <ul class="menu-list list-unstyled">
          <li @click="isOpen = !isOpen">
            <RouterLink to="/" class="menu-link" :class="{ 'active': $route.path === '/' }">
              <span>Home</span>
            </RouterLink>
          </li>
          <li @click="isOpen = !isOpen">
            <RouterLink to="/myself" class="menu-link" :class="{ 'active': $route.path === '/myself' }">
              <span>Myself</span>
            </RouterLink>
          </li>
          <li>
            <RouterLink to="/" class="menu-link" :class="{ 'active': $route.path === '' }">
              <span>About</span>
            </RouterLink>
          </li>
          <li>
            <RouterLink to="/" class="menu-link" :class="{ 'active': $route.path === '' }">
              <span>Contact</span>
            </RouterLink>
          </li>
        </ul>
        <div class="nav-contact me-md-5">
          <a target="_blank" href="https://github.com/MOEN-ERAK" class="contact-item">
            <Icon icon="mingcute:github-fill" width="35" height="35" class="icon" />
            <span>MOEN-ERAK</span>
          </a>
          <a target="_blank" href="mailto:raknosmoke000@gmail.com" class="contact-item">
            <Icon icon="line-md:email-alt-filled" width="35" height="35" class="icon" />
            <span>Email link
              <Icon icon="lets-icons:copy-light" width="24" height="24" />
            </span>
          </a>
          <a target="_blank" href="https://www.facebook.com/rak.nosmoke.1/" class="contact-item">
            <Icon icon="mingcute:meta-line" width="35" height="35" class="icon" />
            <span>Rak Acoustïc</span>
          </a>
          <a target="_blank" href="https://t.me/MOENERAK" class="contact-item">
            <Icon icon="mingcute:telegram-fill" width="35" height="35" class="icon" />
            <span>@MOENERAK</span>
          </a>
        </div>
      </div>
      <div class="marquee">
        <div class="marquee-content">
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
          <span class="text-light">raknosmok000@gmail.com</span>
        </div>
      </div>
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
    padding: .5rem;
    background-color: black;
    z-index: 9999;
    aspect-ratio: 1/1;
    border: none;
    top: 0;
    right: 0;
    transform: translate(50%, -50%);
    margin: var(--menu-border-gap);
    pointer-events: all;
    width: clamp(40px, 5dvw, 80px);
    display: gird;
    place-items: center;

    .something-wrapper {
      position: inherit;
      inset: 0;
      border-radius: 100%;

      .me-photo {
        position: inherit;
        width: 100%;
        height: 100%;
        overflow: hidden;
        border-radius: 100%;

        img {
          width: 100%;
        }
      }

      .welcome-text {
        position: inherit;
        left: 0;
        top: 50%;
        transform: translate(-120%, -50%);
        border-radius: 0;
        padding: 0 .3rem;
        white-space: nowrap;
        font-size: var(--font-size-sm);

        &::before {
          content: 'Hi, dear!';
        }
      }
    }

    &:focus,
    &:focus-visible {
      border: none;
      outline: none;
    }

    .burger {
      width: 80%;
      height: 8%;
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
    mask-image: radial-gradient(circle at calc(100dvw - var(--menu-border-gap)) calc(0dvh + var(--menu-border-gap)), black 1%, transparent 0%);
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
          font-size: min(20dvh, 25dvw);
          text-decoration: none;
          font-weight: bolder;
          letter-spacing: -.1rem;
          line-height: 100%;
          display: flex;
          column-gap: 2rem;
          position: relative;
          isolation: isolate;

          &::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            z-index: -1;
          }

          &,
          * {
            transition: .3s;
          }

          &.active {
            color: var(--bs-dark);

            &::before {
              background-color: greenyellow;
            }
          }

          &:hover {
            &:not(.active) {
              color: greenyellow;
            }
          }
        }
      }
    }

    .nav-contact {
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 1fr 1fr;
      gap: calc(var(--font-size-sm) - .5rem);
      width: min(50dvh, 100vw);
      align-self: center;

      .contact-item {
        text-decoration: none;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        color: white;
        row-gap: var(--font-size-sm);
        font-size: var(--font-size-sm);
        position: relative;
        overflow: hidden;
        isolation: isolate;
        background-color: var(--bs-dark);

        img {
          width: var(--font-size-xl);
        }

        .icon,
        span {
          transition: .2s;
        }

        &:hover {
          background-color: greenyellow;

          * {
            color: black;
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

.marquee {
  position: relative;
  overflow: hidden;
  white-space: nowrap;
  width: 100%;
  padding: 0.5rem;

  .marquee-content {
    display: inline-block;
    animation: scroll 20s linear infinite;

    span {
      display: inline-block;
      font-size: var(--font-size-base);
      color: #eee;
      display: inline-flex;
      align-items: center;

      &::after {
        content: '';
        width: 10px;
        aspect-ratio: 1/1;
        background-color: greenyellow;
        border-radius: 100%;
        margin-inline: var(--font-size-sm);
      }
    }
  }
}



@keyframes scroll {
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(-50%);
  }
}

@keyframes border-rotate {
  to {
    transform: rotate(360deg);
  }
}

@media (min-width: 768px) {
  .contact-item {
    aspect-ratio: 1/1;
    width: auto;
  }
}
</style>
