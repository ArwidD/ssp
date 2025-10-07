<script setup>
import { ref, watch } from 'vue'

const props = defineProps(['valdaKnappar', 'reset'])
const emit = defineEmits(['vinnare'])
const resultat = ref('låt spelet börja!')

watch(props, () => {
  console.log('Resultat ändrat till:', props.valdaKnappar)
  if (props.valdaKnappar.spelare === props.valdaKnappar.dator) {
    resultat.value = 'Oavgjort!'
  } else if (props.valdaKnappar.spelare % 2 == props.valdaKnappar.dator % 2) {
    //samma paritet - högsta talet vinner
    if (props.valdaKnappar.spelare > props.valdaKnappar.dator) {
      resultat.value = 'Du vann!'
      emit('vinnare', 'spelare')
    } else {
      resultat.value = 'Datorn vann!'
      emit('vinnare', 'dator')
    }
  } else {
    //olika peritet - lägsta talet vinner
    if (props.valdaKnappar.spelare < props.valdaKnappar.dator) {
      resultat.value = 'Du vann!'
      emit('vinnare', 'spelare')
    } else {
      resultat.value = 'Datorn vann!'
      emit('vinnare', 'dator')
    }
  }
})

watch(
  () => props.reset,
  () => {
    if (props.reset) {
      resultat.value = 'låt spelet börja!'
    }
  },
)
</script>
<template>
  <div class="resultat">
    <p id="resultat">{{ resultat }}</p>
  </div>
</template>
<style scoped>
.resultat {
  font-size: 1.2em;
  text-align: center;
  margin: 1.2em 0;
}
</style>
