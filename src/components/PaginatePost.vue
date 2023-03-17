<script setup>
  const emit = defineEmits(['prevEmit', 'nextEmit']);

  defineProps(["inicio", "fin", "maxLength"]);

  const activarSiguiente = () => {
    console.log('me diste en siguiente');
    emit('nextEmit');
  }
</script>
<template>
    <div class="btn-group" role="group" aria-label="Basic BtnGruoup">
        <button @click="$emit('prevEmit')" type="button" class="btn btn-primary" :disabled="inicio<=0">Previous {{ inicio }}</button>

        <button @click="$emit('nextEmit')" type="button" class="btn btn-primary" :disabled="fin>=maxLength">Next  {{ fin }}</button>
        <!-- <button @click="activarSiguiente()" type="button" class="btn btn-primary">NextConFuncion</button> -->

       

    </div>
</template>
