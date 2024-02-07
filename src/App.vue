<script setup>
import { gsap } from "gsap";
import { onMounted, ref } from 'vue'

onMounted(() => {
  // Example 1
  gsap.from('.imgNagai', { x: 400, y: 200, opacity: 0, scale: .5, skewX: 60, skewY: 30, rotate: -30, duration: 2 })
  // gsap.from('.titExotic', { x: 550, opacity: 0, stagger: .3, duration: 2, delay: .3 })

  // Example 2 : repeat, yoyo
  // gsap.to('.titExotic:nth-child(1)', { x: 200, duration: 1, repeat: 1, })
  // gsap.to('.titExotic:nth-child(2)', { x: 200, duration: 1, repeat: -1, })
  // gsap.to('.titExotic:nth-child(3)', { x: 200, duration: 1, repeat: -1, yoyo: true })

  // Example 3: easing
  // gsap.to('.titExotic:nth-child(1)', { x: 300, duration: 2, repeat: -1, ease: "back.inOut(8)" })
  // gsap.to('.titExotic:nth-child(2)', { x: 300, duration: 2, repeat: -1, ease: "bounce" })
  // gsap.to('.titExotic:nth-child(3)', { scale: 2, x: 1000, opacity: 0, duration: 2, repeat: -1, ease: "slow(0.7,0.7,false)" })

  // Example 4 : stagger
  // gsap.to('.titExotic', { x: 300, repeat: -1, stagger: .15, ease: "power1.inOut", yoyo: true })
  // gsap.to('.titExotic', {
  //   x: 300, repeat: -1, stagger: {
  //     each: 0.2,
  //     from: "center"
  //   }, ease: "power1.inOut", yoyo: true
  // })

  // Example 5: tween control
  const btnPlay = document.getElementById('play')
  const btnPause = document.getElementById('pause')
  const btnReverse = document.getElementById('reverse')
  const btnRestart = document.getElementById('restart')
  const btnGoToSeconds = document.getElementById('goToSeconds')
  const btnGoToPercent = document.getElementById('goToPercent')
  const btnHalfSpeed = document.getElementById('halfSpeed')
  const btnToEndReverseDoubleSpeed = document.getElementById('toEndReverseDoubleSpeed')
  const btnKillTween = document.getElementById('killTween')
  const goToLabel = document.getElementById('goToLabel')
  //   let tween = gsap.to('.titExotic:nth-child(1)', { x: 600, duration: 3, ease: "linear", paused: true })
  //   btnPlay.addEventListener('click', () => tween.play())
  //   btnPause.addEventListener('click', () => tween.pause())
  //   btnReverse.addEventListener('click', () => tween.reverse())
  //   btnRestart.addEventListener('click', () => tween.restart())
  //   btnGoToSeconds.addEventListener('click', () => tween.seek(0.5))
  //   btnGoToPercent.addEventListener('click', () => tween.progress(0.75))
  //   btnHalfSpeed.addEventListener('click', () => tween.timeScale(0.5))
  //   btnToEndReverseDoubleSpeed.addEventListener('click', () => tween.progress(1).timeScale(2).reverse())
  //   btnKillTween.addEventListener('click', () => tween.kill())

  // Example 6: transform origin & how to edit your tween config
  const btnsTransform = document.querySelectorAll('.btnTransform')
  const tween = gsap.to('.imgPlants', { rotate: 360, duration: 2, paused: true })
  function changeTransformOriginAndPlay(value) {
    // When you invalidate() an animation, it will be re-initialized the next time it renders and its vars object will be re-parsed
    tween.pause().progress(0).invalidate()
    tween.vars.transformOrigin = value
    tween.play()
  }
  btnsTransform.forEach(btn => {
    btn.addEventListener('click', (e) => {
      changeTransformOriginAndPlay(e.target.dataset.transform)
    })
  })

  // Example 7: invalidate()
  const btnRestartTealSquare = document.getElementById('restartTealSquare')
  const btnInvalidateAndRestartTealSquare = document.getElementById('invalidateAndRestartTealSquare')
  const tealSquareTween = gsap.to('.tealSquare', { x: "+=100px", duration: 1, paused: true })
  btnRestartTealSquare.addEventListener('click', () => tealSquareTween.restart())
  btnInvalidateAndRestartTealSquare.addEventListener('click', () => {
    tealSquareTween.invalidate().restart()
  })

  // Example 8
  const animation = gsap.timeline()
    .from('#titles', { opacity: 0, x: 400 })
    .from('.titExotic', { scale: .3, ease: "back", transformOrigin: "center left", stagger: .4 }, "+=0.5")
    .to('.titExotic:nth-child(3)', { scale: 2, rotate: 180, ease: "back", transformOrigin: "center", yoyo: true, repeat: 1 }, 2)
    .add("labelTest")
    .to('.titExotic:nth-child(2)', { xPercent: 100, delay: .1 }, 2)

  btnPlay.addEventListener('click', () => animation.play())
  btnPause.addEventListener('click', () => animation.pause())
  btnReverse.addEventListener('click', () => animation.reverse())
  btnRestart.addEventListener('click', () => animation.restart())
  btnGoToSeconds.addEventListener('click', () => animation.seek(0.5))
  btnGoToPercent.addEventListener('click', () => animation.progress(0.75))
  btnHalfSpeed.addEventListener('click', () => animation.timeScale(0.5))
  btnToEndReverseDoubleSpeed.addEventListener('click', () => animation.progress(1).timeScale(2).reverse())
  goToLabel.addEventListener('click', () => animation.play("labelTest"))

})
</script>

<template>
  <div class="bg-slate-800 text-white min-h-screen ">
    <section>
      <div class="imgNagai">
        <img class="w-full h-full object-cover" src="/hiroshinagai01.jpg" alt="">
      </div>
    </section>
    <section class="p-6 overflow-clip">
      <div id="titles" class="flex flex-col items-start">
        <h1 class="titExotic text-7xl font-serif">Exotic Plants</h1>
        <h1 class="titExotic text-7xl font-serif">Exotic Plants</h1>
        <h1 class="titExotic text-7xl font-serif">Exotic Plants</h1>
        <h1 class="titExotic text-7xl font-serif">Exotic Plants</h1>
        <h1 class="titExotic text-7xl font-serif">Exotic Plants</h1>
      </div>
      <div class="flex gap-2 mt-4">
        <button id="play" class="px-3 py-1 bg-orange-500 text-white rounded-md">Play</button>
        <button id="pause" class="px-3 py-1 bg-orange-500 text-white rounded-md">Pause</button>
        <button id="reverse" class="px-3 py-1 bg-orange-500 text-white rounded-md">Reverse</button>
        <button id="restart" class="px-3 py-1 bg-orange-500 text-white rounded-md">Restart</button>
        <button id="goToSeconds" class="px-3 py-1 bg-orange-500 text-white rounded-md">Go to 0.5s in</button>
        <button id="goToPercent" class="px-3 py-1 bg-orange-500 text-white rounded-md">Go to 75% in</button>
        <button id="halfSpeed" class="px-3 py-1 bg-orange-500 text-white rounded-md">Play half speed</button>
        <button id="toEndReverseDoubleSpeed" class="px-3 py-1 bg-blue-500 text-white rounded-md">Play from end in
          reverse @double speed</button>
        <button id="killTween" class="px-3 py-1 bg-red-500 text-white rounded-md">Kill tween</button>
        <button id="goToLabel" class="px-3 py-1 bg-pink-500 text-white rounded-md">Go to Label</button>
      </div>
      <div class="mt-12">
        <div class="tealSquare w-20 h-20 bg-teal-500 rounded-md"></div>
        <button class="px-3 py-1 bg-orange-500 text-white rounded-md" id="restartTealSquare">Restart</button>
        <button class="px-3 py-1 bg-orange-500 text-white rounded-md ml-2" id="invalidateAndRestartTealSquare">Invalidate
          and
          restart</button>
      </div>
      <div class="relative h-96 w-96 mx-auto mt-20">
        <img class="imgPlants w-full h-full object-contain" src="/exoticplants02-nobg.webp" alt="">
        <div class="absolute top-0 left-0 z-10 w-full h-full">
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-0 left-0"
            data-transform="0% 0%">0%
            0%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-0 left-1/2"
            data-transform="50% 0%">50%
            0%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-0 left-full"
            data-transform="100% 0%">100%
            0%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-1/2 left-0"
            data-transform="0% 50%">0%
            50%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2"
            data-transform="50% 50%">50%
            50%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-1/2 left-full"
            data-transform="100% 50%">100%
            50%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-full left-0"
            data-transform="0% 100%">0%
            100%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-full left-1/2"
            data-transform="50% 100%">50%
            100%</button>
          <button
            class="btnTransform w-max px-3 py-1 bg-teal-500/50 text-white rounded-md absolute -translate-x-1/2 -translate-y-1/2 top-full left-full"
            data-transform="100% 100%">100%
            100%</button>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.imgNagai {
  height: 450px;
  width: 450px;
}
</style>
