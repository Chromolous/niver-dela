<script setup lang="ts">
import { computed, ref } from 'vue'
import yipe from '../assets/yipee.m4a'

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
        openCurtain()
    } else {
        contadorPresente++
        scale.value++
    }
    
}

function prox_pagina() {
    page.value++
}

const mensagem1 = `
Oi Carla, quanto tempo né? Se pa você ta meio perdida, mas vai fazer sentido (eu acho).\n
Primeiramente, parabéns pelo o seu dia! 17 anos? Me perdi na conta.\n
A gente era criança quando nos conhecemos e agora eu to me sentindo um velho. "Ai mas você sempre foi meio idoso" xiu, não ligo`

const msg1Array = computed(() => mensagem1.split(''))

</script>

<template>
  <div class="relative h-screen w-screen overflow-hidden" :class="{ 'shake-container':shake }">
    <div class="absolute inset-0 overflow-hidden z-0 pointer-events-none">
        <div class="aurora"></div>
        <div class="aurora opacity-50"></div>
    </div>

    <div class="relative z-1 flex flex-col items-center justify-center h-full">
        <h1 v-if="page == 0" class="text-neutral-200 z-10">FELIZ ANIVERSÁRIO</h1>
        <h1 v-if="page == 1" class="text-neutral-200 z-10">
            <span
                v-for="(char, index) in 'Mas antes, uma mensagem especial'.split('')"
                :key="index"
                class="inline-block opacity-0 animate-fadeIn"
                :style="{ animationDelay: index * 0.05 + 's' }">
                <template v-if="char === '\n'">
                    <br>
                </template>
                <template v-else>
                    {{ char === ' ' ? '\u00A0' : char }}
                </template>
            </span>
        </h1>
        <div v-if="page == 2" class="bg-black/20 w-1/2 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <span
                    v-for="(char, index) in msg1Array"
                    :key="index"
                    class="inline-block opacity-0 animate-fadeIn"
                    :style="{ animationDelay: index * 0.03 + 's' }">
                    <template v-if="char === '\n'">
                        <br>
                    </template>
                    <template v-else>
                        {{ char === ' ' ? '\u00A0' : char }}
                    </template>
                </span>
            </p>
        </div>
        
        <button @click="prox_pagina()" class="bg-white opacity-85 rounded-xl px-6 py-3 shadow-lg hover:cursor-pointer active:scale-90 transition duration-100">
            Continuar...
        </button>
    </div>

    <!--E tome confete-->

    <div v-if="page < 2" class="absolute inset-0 pointer-events-none z-10">
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
