<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import Teste from './components/Teste.vue'
import { ref } from 'vue'

const ativo = ref(true)
</script>

<template>
  <Teste v-if="ativo" />
  <HelloWorld v-if="!ativo"/>
</template>
