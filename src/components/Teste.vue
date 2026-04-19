<script setup lang="ts">
import { ref } from 'vue'
import yipe from '../assets/yipee.m4a'
import boom from '../assets/BOOM.m4a'

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
    if (page.value == 10) {
        new Audio(yipe).play();

    }
}

const mensagem1 = `Oi Carla, quanto tempo né? Se pa você ta meio perdida, mas vai fazer sentido (eu acho).
Primeiramente, parabéns pelo o seu dia! 17 anos? Me perdi na conta.
A gente era criança quando nos conhecemos e agora eu to me sentindo um velho.
"Ai mas você sempre foi meio idoso" fala isso na minha cara, covarde.`.split('')

const mensagem2 = `Bom, nós paramos de nos falar de uma forma... inadequada eu diria. 
Então eu queria acertar os assuntos com você :)
Sendo assim...
`.split('')

const mensagem3 = `EU NÃO DISSE NADA!!!`

const mensagem4 = `Quando eu tomei block eu fui procurar saber o que tinha acontecido, e me falaram que a praga do Davi espalhou
MENTIRAS
DESINFORMAÇÃO
CALÚNIAS 
sobre coisas que eu falei ou deixei de falar, e imaginei que esse tivesse sido o motivo para acontecer o que aconteceu.
`

const mensagem5 = `De fato, na época nós estávamos criando uma distancia aos poucos por... vários motivos.
Mas nada que me fizesse desgostar de você ou falar mal de você!
`

const mensagem6 = `Enfim, nem sei se esse foi realmente o estopim para a sua decisão, mas agora já passou tanto tempo que tanto faz.
E já que a gente parou de se falar, eu queria pelo menos fazer isso de um jeito menos zoado.
`

const mensagem7 = `É fato que ambos já participamos consideravelmente da vida um do outro, seja por bem ou por mal,
e é por isso que eu gostaria que tivessemos boas memórias um do outro.
Pensando nisso eu...
bom
er
meio que tipo assim
eu ia fazer um mega compilado de coisas nossas (fotos, vídeos, mensagens e etc)
mas como eu sou um procrastinador top 10 eu acabei deixando pra depois e esquecendo.
ops.
`

const mensagem8 = `MAS DE QUALQUER FORMA
Sinto muito por todos os momentos ruins e queria te agradecer por todos os momentos bons que você proporcionou.
Você é uma menina muito dedicada, talentosa, gentil e eu até poderia ficar citando todas as suas qualidades,
mas aí você teria que ficar clicando nesse botão de continuar por um tempinho.
`

const mensagem9 = `Acho que é mais ou menos isso, essa provavelmente é a minha última mensagem pra você (ou pelo menos uma das últimas)
Tchau Cah! Fica bem, espero todo sucesso do mundo pra você!
`

</script>

<template>
  <div class="relative h-screen w-screen overflow-hidden" :class="{ 'shake-container':shake }">
    <div class="absolute inset-0 overflow-hidden z-0 pointer-events-none">
        <div class="aurora"></div>
        <div class="aurora opacity-50"></div>
    </div>

    <div class="relative z-1 flex flex-col items-center justify-center h-full">
        <h1 v-if="page == 0" class="text-neutral-200 z-10">FELIZ ANIVERSÁRIO</h1>

        <div v-if="page == 1" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem1" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <div v-if="page == 2" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem2" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <h1 v-if="page == 3" class="text-neutral-200 font-bold">
            {{mensagem3}}
        </h1>

        <div v-if="page == 4" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem4" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <div v-if="page == 5" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem5" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <div v-if="page == 6" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem6" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <div v-if="page == 7" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem7" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <div v-if="page == 8" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem8" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <div v-if="page == 9" class="bg-black/20 w-16/20 h-fit rounded-lg py-2 px-2 mb-5">
            <p class="text-neutral-200">
                <template v-for="(char, index) in mensagem9" :key="index">
                    <br v-if="char === '\n'" />
                    <span v-else class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: index * 0.01 + 's' }">
                        {{ char === ' ' ? '\u00A0' : char }}
                    </span>
                </template>
            </p>
        </div>

        <h1 v-if="page == 10" class="text-neutral-200 font-bold">
            <span class="inline-block opacity-0 animate-fadeIn" :style="{ animationDelay: 0.1 + 's' }">
                Feito com ❤ por "Jossoares" (ou "jossoaris?")
            </span>
        </h1>
        
        <button v-if="page < 10" @click="prox_pagina()" class="bg-white opacity-85 rounded-xl px-6 py-3 shadow-lg hover:cursor-pointer active:scale-90 transition duration-100">
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
