<script setup>
import { ref } from 'vue'
import KnappRad from './components/KnappRad.vue'
import ResultatRad from './components/ResultatRad.vue'
import PoangRad from './components/PoangRad.vue'

const knappar = ref(['Sten', 'Sax', 'Påse'])
const score = ref({ spelare: 0, dator: 0 })
const resultat = ref('Du vann!')
const vinnare = ref('')

function hittaVinnare(valdaKnappar) {
  vinnare.value = ''
  let spelare = knappar.value.indexOf(valdaKnappar.spelare)
  let dator = knappar.value.indexOf(valdaKnappar.dator)

  resultat.value = { spelare: spelare, dator: dator }
}

function reset() {
  score.value.dator = 0
  score.value.spelare = 0
  let buttons = document.getElementsByClassName('alternativ')
  for (let b of buttons) {
    b.title = ''
    b.classList.remove('spelarval')
    b.classList.remove('datorval')
  }
}

function raknaPoang(v) {
  if (v === 'spelare') {
    score.value.spelare++
  } else {
    score.value.dator++
  }
  vinnare.value = v
}
</script>

<template>
  <header>
    <h1>Sten, sax, påse</h1>
  </header>

  <main>
    <KnappRad :knappar="knappar" @valda-Knappar="hittaVinnare" />
    <ResultatRad :valda-Knappar="resultat" @vinnare="raknaPoang" />
    <PoangRad :vinnare="vinnare" />

    <button id="nolla" @click="reset">Nollställ poäng</button>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  margin-bottom: 1.2em;
}

#nolla {
  margin-top: 2em;
  padding: 0.3em 0.6em;
  font-size: 0.8em;
}
</style>
