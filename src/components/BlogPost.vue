<script setup>
    //const props = defineProps(['id', 'title', 'subtitle', 'body', 'colorText']);
    //console.log(props.id+" - "+props.title+" - "+props.subtitle);

    defineProps({
        id: Number,
        title: String,
        subtitle: String,
        body: {
            type: String,
            default: "Sin descripcion",
        },
        colorText: String,
        cambiarFavorito: Function
    });

    // defineEmits(['cambiarFavoritoNombre'])
    // const emit = defineEmits(['cambiarFavoritoNombre']);

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h4 class="card-title" :class="`text-${colorText}`">{{id}} - {{title}}</h4>
            <h6 class="card-title">{{subtitle}}</h6>
            <p>{{body}}</p>
            <!-- <button @click="emit('cambiarFavoritoNombre', title)" class="btn btn-outline-primary">Favorito</button> -->
            <button @click="cambiarFavorito(id)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>