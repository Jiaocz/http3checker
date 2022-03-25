<template>
  <div class="container">
    <div class="inner-container">
      <div class="checker-container">
        <component :is="component" />
      </div>
      <div class="logo-container">
        <img src="../assets/orange.png" alt="orange" />
      </div>
    </div>
    <footer>
      <p>
        <a href="https://orangii.cn" target="_blank">&copy; Orangii|橙梓</a>
        <a href="https://orangii.cn/friends" target="_blank">友情链接</a>
      </p>
    </footer>
  </div>
</template>

<script setup>
import { onMounted, shallowRef } from "vue";
import Checking from './Checking.vue'
import Success from './Success.vue'
import Failed from './Failed.vue'
import axios from 'axios'

let component = shallowRef(Checking)

onMounted(async () => {
  let res = await axios.get('test.json', {
    headers: {
      "Cache-Control": "no-cache"
    }
  });
  if(res.headers['x-quic'] === 'h3' || res.headers['x-quic'] === 'hq') {
    component.value = Success
  } else {
    component.value = Failed
  }
})

</script>

<style scoped lang="less">
.container {
  position: relative;
  padding: 5rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;

  background-image: linear-gradient(to bottom, rgba(255, 255, 255, .05), rgba(255, 255, 255, .05),), url("../assets/bg.jpg");
  background-size: cover;
  background-position: center center;
}

.inner-container {
  position: relative;
  height: 100%;
  width: 60%;
  min-width: 300px;

  @media screen and (max-width: 768px) {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}

.checker-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 90%;
  height: 100%;
  z-index: 3;
  padding: 1.25rem 0;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;

  @media screen and (max-width: 768px) {
    position: relative;
    width: 100%;
    height: 60%;
  }

  border: 2px solid rgba(255, 255, 255, 0.6);
  border-radius: 5px;
  background-image: linear-gradient(0deg, rgba(255, 255, 255, 0.4), rgba(243, 245, 248, 0.4));
  box-shadow: 8px 8px 20px 0 rgb(55 99 170 / 10%), -8px -8px 20px 0 rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(12px);
  transition: all .2s ease-in-out;

  &:hover {
    box-shadow: 8px 8px 20px 0 rgb(55 99 170 / 20%), -8px -8px 20px 0 rgba(255, 255, 255, 0.75);
  }
}

.logo-container {
  position: absolute;
  top: -15px;
  right: 0;
  width: 35%;
  z-index: 2;
  transform: rotate(80deg) scale(1.5);

  animation: logo-animation 10s ease-in-out infinite;
}

footer {
  position: absolute;
  bottom: 10px;

  a {
    color: #2c3e50;
    text-decoration: none;

    &:not(:first-child)::before {
      content: '|';
      margin: auto 0.2em;
      user-select: none;
      pointer-events: none;
    }
  }
}
</style>
<style>
@keyframes logo-animation {
  0%, 100% {
    transform: rotate(80deg) scale(1.5);
  }
  50% {
    transform: translate(15px, -15px) rotate(80deg) scale(1.5);
  }
}
</style>
