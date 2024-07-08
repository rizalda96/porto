<template>
  <div class="page-transition">
    <div
      class="page-transition__red left-0 top-0 absolute h-screen w-screen bg-red-950"
      ref="transition__red"
    ></div>
    <div
      class="page-transition__black left-0 top-0 absolute h-screen w-screen bg-black"
      ref="transition__black"
    ></div>
    <div
      class="transition__logo uppercase text-6xl z-[1] absolute text-white font-bold top-[50vh] left-[50vw] -translate-x-1/2 -translate-y-1/2"
    >
      I'M LOGO
    </div>
  </div>

  <button
    id="button"
    class="bottom-[15vh] left-[5vw] uppercase text-base z-[1] text-cyan-300 bg-transparent p-5 border border-sky-500"
    @click.prevent="playAnimation"
  >
    TRANSITION
  </button>
</template>

<script setup>
import gsap from 'gsap'

const tl = gsap.timeline({ paused: true }) // Create timeline outside of onMounted

onMounted(() => {
  // Initialize animations within onMounted
  tl.fromTo(
    '.page-transition__red',
    { scaleX: 0 },
    { scaleX: 1, transformOrigin: 'right', ease: 'easeInOut', duration: 1 }
  )
    .fromTo(
      '.page-transition__black',
      { scaleX: 0 },
      { scaleX: 1, transformOrigin: 'right', ease: 'easeInOut', duration: 1.5 },
      0.2
    )
    .fromTo(
      '.transition__logo',
      { xPercent: -100, autoAlpha: 0 },
      { xPercent: 0, autoAlpha: 1, ease: 'easeInOut', duration: 0.5 },
      0.5
    )
    .set('.page-transition__red', { scaleX: 0 })
    .to('.transition__logo', { autoAlpha: 0, duration: 0.5 }, '-=0.5')
    .to('.page-transition__black', {
      scaleX: 0,
      transformOrigin: 'left',
      ease: 'easeInOut',
      duration: 1
    })
})

const playAnimation = () => {
  tl.restart()
}

defineExpose({
  playAnimation
})
</script>

<style lang="scss" scoped></style>
