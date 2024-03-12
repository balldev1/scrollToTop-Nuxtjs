<template>
  <div class="w-full  bg-black">
    <button class="scroll-to-top-top hover:scale-110" @click="scrollToTop">↑</button>
    <button class="scroll-to-top-start" @click="scrollToStart"><a>start</a></button>
    <button class="scroll-to-top-center" @click="scrollToCenter"><a>center</a></button>
    <button class="scroll-to-top-end" @click="scrollToEnd"><a>end</a></button>
    <div class="navbar bg-base-100">
      <div class="flex-1">
        <a class="btn btn-ghost text-xl">daisyUI</a>
      </div>
      <div class="flex-none">
        <ul class="menu menu-horizontal px-1">
          <li  @click="scrollToTop"><a>home</a></li>
          <li @click="scrollToStart"><a>start</a></li>
          <li  @click="scrollToCenter"><a>center</a></li>
          <li @click="scrollToEnd"><a>end</a></li>
        </ul>
      </div>
    </div>

    <div class="flex flex-col space-y-[30dvw]">
      <div id="start">
        start
      </div>
      <div id="center">
        center
      </div>
      <div id="end">
        end
      </div>
    </div>
  </div>

</template>

<script setup lang="ts">
import { ref } from 'vue';

const showScrollBtn = ref(false);

// scroll
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
}

const scrollToStart = () => {
  const contactElement = document.getElementById('start');
  if (contactElement) {
    scrollToElement(contactElement);
  }
}
const scrollToCenter = () => {
  const contactElement = document.getElementById('center');
  if (contactElement) {
    scrollToElement(contactElement);
  }
}
const scrollToEnd = () => {
  const contactElement = document.getElementById('end');
  if (contactElement) {
    scrollToElement(contactElement);
  }
}

const scrollToElement = (element: HTMLElement) => {
  const duration = 1000; // Adjust duration (milliseconds) as needed
  const targetPosition = element.getBoundingClientRect().top + window.pageYOffset;
  const startPosition = window.pageYOffset;
  let startTime: number | null = null;

  const animation = (currentTime: number) => {
    if (startTime === null) startTime = currentTime;
    const timeElapsed = currentTime - startTime;
    const scrollAmount = easeInOutQuad(timeElapsed, startPosition, targetPosition - startPosition, duration);
    window.scrollTo(0, scrollAmount);
    if (timeElapsed < duration) requestAnimationFrame(animation);
  };

  const easeInOutQuad = (t: number, b: number, c: number, d: number) => {
    t /= d / 2;
    if (t < 1) return c / 2 * t * t + b;
    t--;
    return -c / 2 * (t * (t - 2) - 1) + b;
  };

  requestAnimationFrame(animation);
}

const handleScroll = () => {
  const scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
  showScrollBtn.value = scrollTop > 0;
}





import { onMounted } from 'vue';

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});
</script>

<style scoped>

.scroll-to-top-top {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 20px;
  cursor: pointer;
  display: none;
}

.scroll-to-top-end {
  position: fixed;
  bottom: 70px;
  right: 20px;
  margin-bottom: 10px; /* กำหนดระยะห่างระหว่างปุ่ม */
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 20px;
  cursor: pointer;
  display: none;
}

.scroll-to-top-center {
  position: fixed;
  bottom: 130px; /* คำนวณตำแหน่งตามขนาดของปุ่มและระยะห่าง */
  right: 20px;
  margin-bottom: 10px; /* กำหนดระยะห่างระหว่างปุ่ม */
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 20px;
  cursor: pointer;
  display: none;
}

.scroll-to-top-start {
  position: fixed;
  bottom: 190px; /* คำนวณตำแหน่งตามขนาดของปุ่มและระยะห่าง */
  right: 20px;
  margin-bottom: 10px; /* กำหนดระยะห่างระหว่างปุ่ม */
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 20px;
  cursor: pointer;
  display: none;
}

.w-full:hover .scroll-to-top-top,
.w-full:focus .scroll-to-top-top {
  display: block;
}

.w-full:hover .scroll-to-top-start,
.w-full:focus .scroll-to-top-start {
  display: block;
}

.w-full:hover .scroll-to-top-center,
.w-full:focus .scroll-to-top-center {
  display: block;
}
.w-full:hover .scroll-to-top-end,
.w-full:focus .scroll-to-top-end {
  display: block;
}
</style>