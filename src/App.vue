<template>
  <main class="min-vh-100 d-flex align-items-center justify-content-center">
    <div class="container">
      <div class="quote-box position-relative px-4 py-4 rounded-3 w-50 text-center mx-auto">
        <span class="text-uppercase fw-bold">Advice #{{ advice.id }}</span>
        <p class="quote my-4 px-4 fw-bold">
          “{{ advice.advice }}”
        </p>
        <img class="desk w-100 mt-3 mb-5" src="/images/pattern-divider-desktop.svg" alt="">
        <img class="mobile d-none w-100 mt-3 mb-5" src="/images/pattern-divider-mobile.svg" alt="">
        <div class="dic-button" @click="generator">
          <img src="/images/icon-dice.svg" alt="">
        </div>
      </div>
    </div>
  </main>
</template>
<script setup>
import { ref, onMounted } from 'vue';

const advice = ref({})

const generator = () => {
  fetch('https://api.adviceslip.com/advice')
    .then(response => response.json())
    .then(data => {
      console.log(data.slip);
      advice.value = data.slip
    })
}

onMounted(() => {
  fetch('https://api.adviceslip.com/advice')
    .then(response => response.json())
    .then(data => {
      console.log(data.slip);
      advice.value = data.slip
    })
})

</script>
<style lang="scss">
* {
  box-sizing: border-box;
}

:root {
  // ### Primary
  --Light-Cyan: hsl(193, 38%, 86%);
  --Neon-Green: hsl(150, 100%, 66%);

  // ### Neutral
  --Grayish-Blue: hsl(217, 19%, 38%);
  --Dark-Grayish-Blue: hsl(217, 19%, 24%);
  --Dark-Blue: hsl(218, 23%, 16%);
}

body {
  background-color: var(--Dark-Blue);
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

p.quote {
  font-size: 28px;
}

main {
  .quote-box {
    background-color: var(--Dark-Grayish-Blue);
    box-shadow: 0 5px 20px #20202070;

    span {
      color: var(--Neon-Green);
      letter-spacing: 3px;
      font-size: 12px;
    }

    .quote {
      color: var(--Light-Cyan);
    }

    .dic-button {
      background-color: var(--Neon-Green);
      width: fit-content;
      border-radius: 50%;
      width: 60px;
      height: 60px;
      display: flex;
      margin: auto;
      position: absolute;
      bottom: -30px;
      left: 50%;
      transform: translateX(-50%);
      align-items: center;
      justify-content: center;
      transition: 0.2s;
      cursor: pointer;

      img {
        transition: 0.2s;
      }

      &:hover {
        img {
          transform: rotate(45deg);
        }

        box-shadow: 0 0 30px var(--Neon-Green);
      }
    }
  }

  @media (max-width: 767px) {
    .desk {
      display: none;
    }
    .mobile {
      display: block !important;
    }
    .quote-box {
      width: 100% !important;
      p {
        padding: 0 0 !important;
      }
    }
  }
}
</style>