<script setup lang="ts">
import { ref } from 'vue'
import yipe from '../assets/yipee.m4a'
import boom from '../assets/BOOM.m4a'
import aniversariu from '../assets/aniversariu.m4a'

const isOpen = ref(false)
const temConfete = ref(false)
const shake = ref(false)

const page = ref(0)

function openCurtain() {
  isOpen.value = true
  temConfete.value = true
  new Audio(yipe).play();

}

function configConfete() {
  const colors = ['#ff0', '#f0f', '#0ff', '#0f0', '#f00']

  return {
    left: Math.random() * 100 + 'vw',
    backgroundColor: colors[Math.floor(Math.random() * colors.length)],
    animationDuration: (Math.random() * 3 + 2) + 's',
    animationDelay: Math.random() * 5 + 's'
  }
}

let contadorPresente = 0
let scale = ref(1)
function abrePresente() {
    if (contadorPresente >= 7) {
        new Audio(boom).play();
        openCurtain()
    } else {
        contadorPresente++
        scale.value++
    }
    
}

function prox_pagina() {
    page.value++
    if (page.value == 3) {
        new Audio(boom).play();
    }
    if (page.value == 1) {
        new Audio(aniversariu).play();
    }
    if (page.value == 2) {
        new Audio(yipe).play();

    }
}

const mensagem1 = `Feliz aniversário ma sœur (é assim mesmo?), tamo J
Infelizmente não vou estar aí esse ano, mas vamo ve essa meta aí
love u`.split('');

</script>

<template>
  <div class="relative h-screen w-screen overflow-hidden" :class="{ 'shake-container':shake }">
    <div class="absolute inset-0 overflow-hidden z-0 pointer-events-none">
        <div class="aurora"></div>
        <div class="aurora opacity-50"></div>
    </div>

    <div class="relative z-1 flex flex-col items-center justify-center h-full">
        <h1 v-if="page == 0" class="text-neutral-200 z-10">FELIZ ANIVERSÁRIO</h1>

        <div v-if="page == 1" class="bg-black/20 w-12/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem1" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <h1 v-if="page == 2" class="text-neutral-200 font-bold">
            <span class="opacity-0 animate-fadeIn" :style="{ animationDelay: 0.1 + 's' }">
                Feito com ❤ por lele11458
            </span>
            <br>
            <span class="opacity-0 animate-fadeIn" :style="{ animationDelay: 0.5 + 's' }" style="font-size:20px">(AKA eu mesmo)</span>
        </h1>
        
        <button v-if="page < 2" @click="prox_pagina()" class="bg-white opacity-85 rounded-xl px-6 py-3 shadow-lg hover:cursor-pointer active:scale-90 transition duration-100">
            Continuar...
        </button>
    </div>

    <!--E tome confete-->

    <div v-if="page < 1 || page == 10" class="absolute inset-0 pointer-events-none z-10">
        <div
            v-for="i in 40"
            :key="i"
            class="confete"
            :style="configConfete()">
        </div>
    </div>

    
    <div class="absolute inset-0 flex z-10 pointer-events-none">

      <div
        class="w-1/2 bg-black transition-transform duration-1000"
        :class="isOpen ? '-translate-x-full' : 'translate-x-0'"></div>

      <div
        class="w-1/2 bg-black transition-transform duration-1000"
        :class="isOpen ? 'translate-x-full' : 'translate-x-0'"></div>
    </div>

    <div v-if="!isOpen" class="absolute inset-0 flex flex-col items-center justify-center z-20">
        <h2 class="text-neutral-50">O que é isso?</h2>
        <button
            @click="abrePresente"
            class="text-6xl shadow-lg hover:cursor-pointer hover:rotate-3 hover:scale-110 transition duration-300 active:scale-90"
            :style="{ transform: `scale(${scale})` }">
            🎁
        </button>
    </div>

  </div>
</template>
