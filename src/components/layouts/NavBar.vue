<template>
  <div>
    <section
      :class="`nav-bar fixed bg-black w-1/3 text-white h-screen transform transition-all duration-700 ${isActive ? 'right-0 ' : '-right-full'}`"
    >
      <div class="menu p-28 mt-11">
        <h1 class="uppercase text-gray-400">Navigation</h1>
        <div class="mt-3 mb-4 h-[2px] w-full bg-gray-700 opacity-50"></div>

        <div class="flex flex-col gap-y-10">
          <template v-for="(menu, index) in menus" :key="index">
            <router-link
              to=""
              class="flex gap-x-3 items-center group text-7xl h-full asd"
              :ref="(el) => (refs[index] = el)"
            >
              <div
                class="dot w-[12px] h-[12px] bg-white rounded-full opacity-0 group-hover:opacity-100 transform transition-all"
              ></div>
              <span class="">
                {{ menu.meta.label }}
              </span>
            </router-link>
          </template>
        </div>
      </div>
    </section>

    <div class="flex flex-row justify-between py-5 px-8 items-center">
      <div class="p-1" ref="title" @mousemove="onMove" @mouseleave="onLeave">
        <h1>tes aja</h1>
      </div>
      <button class="relative group" @click="toggleActive">
        <div
          :class="`relative flex overflow-hidden items-center justify-center rounded-full w-[70px] h-[70px] transform transition-all bg-slate-700 ring-0 ring-gray-300 hover:ring-8  ring-opacity-30 duration-200 shadow-md ${isActive ? 'ring-4' : ''}`"
        >
          <div
            class="flex flex-col justify-between w-[25px] h-[25px] transform transition-all duration-300 origin-center overflow-hidden"
          >
            <div
              :class="`bg-white h-[3px] w-9 transform transition-all duration-300 origin-left ${isActive ? 'translate-x-10' : ''}`"
            ></div>
            <div
              :class="`bg-white h-[3px] w-9 rounded transform transition-all duration-300 delay-75 ${isActive ? 'translate-x-10' : ''}`"
            ></div>
            <div
              :class="`bg-white h-[3px] w-9 transform transition-all duration-300 origin-left ${isActive ? 'translate-x-10' : ''} delay-150 `"
            ></div>

            <div
              :class="`absolute items-center justify-between transform transition-all duration-500 top-3 -translate-x-10 ${isActive ? 'translate-x-0 w-12' : ''} flex w-0`"
            >
              <div
                :class="`absolute bg-white h-[3px] w-7 transform transition-all duration-500 rotate-0 delay-300 ${isActive ? 'rotate-45' : ''}`"
              ></div>
              <div
                :class="`absolute bg-white h-[3px] w-7 transform transition-all duration-500 -rotate-0 delay-300 ${isActive ? '-rotate-45' : ''}`"
              ></div>
            </div>
          </div>
        </div>
      </button>
    </div>
  </div>

  <!-- <transitions ref="transition" /> -->
</template>

<script setup>
import gsap from 'gsap'

import Transitions from '@components/layouts/Transition.vue'

const tl = gsap.timeline({ paused: true })

const isActive = ref(false)
const transition = ref(null)

const toggleActive = () => {
  // transition.value.playAnimation()
  // setTimeout(() => {
  //   isActive.value = !isActive.value
  // }, 500)
  tl.restart()

  isActive.value = !isActive.value
}

const menus = ref([
  {
    path: '/',
    name: 'home',
    meta: {
      label: 'Home'
    }
    // component: () => import('../views/AboutView.vue')
  },
  {
    path: '/',
    name: 'about',
    meta: {
      label: 'About'
    }
    // component: () => import('../views/AboutView.vue')
  },
  {
    path: '/',
    name: 'contact',
    meta: {
      label: 'Contact'
    }
    // component: () => import('../views/AboutView.vue')
  }
])
const refs = ref([])
// onMounted(() => {
//   initAnimationMenus()
// })

// function initAnimationMenus() {
//   // Access the elements here
//   refs.value.forEach((el, index) => {
//     // console.log(`Element at index ${index}:`, el)
//     // tl.from(el.$el, { x: 170, ease: 'easeInOut' })
//     // tl.from('.asd', { scaleX: 1, transformOrigin: 'right', ease: 'easeInOut', duration: 1.5 })
//     // gsap.to('.asd', { x: 100, duration: 1 })
//     tl.fromTo(el.$el, { xPercent: 150 }, { xPercent: 0, ease: 'bounce', duration: 1, delay: 0.2 })
//   })
// }

const title = ref(null)
function onMove(e) {
  const { clientX, clientY } = e
  const { offsetHeight, offsetLeft, offsetTop, offsetWidth } = title.value
  const x = clientX - (offsetLeft + offsetWidth / 2)
  const y = clientY - (offsetTop + offsetHeight / 2)
  gsap.to(title.value, { x: x })
  gsap.to(title.value, { y: y })
}

function onLeave(e) {
  gsap.to(title.value, { x: 0 })
  gsap.to(title.value, { y: 0 })
}
</script>

<style lang="scss" scoped></style>
