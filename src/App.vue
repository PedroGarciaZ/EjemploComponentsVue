<!-- Options
<script>
  export default {
    data(){
      return {
        counter: 0
      }
    }, methods:{
      increment(){
        this.counter++;
      }
    }
  }
</script>
-->


<!-- 
  <script>
  import { ref } from 'vue';
  export default {
      setup(){
        const counter = ref(0);

        const increment = () => {
          counter.value ++;
        }

        return {
          counter, increment
        }
      }
  }
</script>
-->

<script setup>
  import ButtonCounter from "./components/ButtonCounter.vue";
  import BlogPost from "./components/BlogPost.vue";
  import { onMounted, ref } from "vue";
  import PaginatePost from "./components/PaginatePost.vue";
  import LoadingSpinner from "./components/LoadingSpinner.vue";
  import { computed } from "@vue/reactivity";

  /*
  const posts = ref([
  
    { id: 1, title : 'Post 1', subtitle: 'Subtitulo 1', body: 'descripcion 1', colorText: 'primary' },
    { id: 2, title : 'Post 2', subtitle: 'Subtitulo 2', body: 'descripcion 2', colorText: 'secondary' },
    { id: 3, title : 'Post 3', subtitle: 'Subtitulo 3', body: 'descripcion 3', colorText: 'success' },
    { id: 4, title : 'Post 4', subtitle: 'Subtitulo 4', body: 'descripcion 4', colorText: 'warning' },
    { id: 5, title : 'Post 5', subtitle: 'Subtitulo 5', colorText: 'danger' },
  ]);
  */
  const posts = ref([]);

  const postXPagina = 10;
  const inicio = ref(0);
  const fin = ref(postXPagina);

  const loading = ref(true);

  const favorito = ref('');

  const cambiarFavorito = (title) => {
    favorito.value = title;
  }

  const prev = () =>{
    inicio.value -= postXPagina;
    fin.value -= postXPagina;
  };

  const next = () =>{
    inicio.value = inicio.value + postXPagina;
    fin.value = fin.value + postXPagina;
  };


  onMounted( async() => {
    fetchData();
  });
  
  const fetchData = async () =>{
    // loading.value = true;
    try{
      const resp = await fetch("https://jsonplaceholder.typicode.com/posts");
      posts.value = await resp.json();
    }catch(error){
      console.log(error);
    }finally{
      setTimeout(()=>{
        loading.value= false;
      }, 1000)
    }
  }

  const maxLength = computed( () => posts.value.length );

</script>
<!-- fetch('https://jsonplaceholder.typicode.com/posts')
.then( resp => resp.json())
.then( data => {
  posts.value= data
}).finally(() => {
  setTimeout(() =>{
    loading.value=false 
  }, 1000);
}); -->

<template>

  <LoadingSpinner v-if="loading"/>

  <div class="container" v-else>

    <h1>Aplicacion de Componentes</h1>

    <h2> Mis Post Favoritos: {{ favorito }}</h2>
  
  <!-- 
    <ButtonCounter/>
    <button-counter></button-counter>  
  -->

  <!-- 
    <BlogPost :id="1" title="Post 1" subtitle="Subtitulo 1" body="descripcion 1" colorText="primary"/>
    <BlogPost :id="2" title="Post 2" subtitle="Subtitulo 2" body="descripcion 2" colorText="secondary"/>
    <BlogPost :id="3" title="Post 3" subtitle="Subtitulo 3" body="descripcion 3" colorText="success"/>
    <BlogPost :id="4" title="Post 4" subtitle="Subtitulo 4" body="descripcion 4" colorText="warning"/>
    <BlogPost :id="5" title="Post 5" subtitle="Subtitulo 5"  colorText="danger"/>
  -->

  <PaginatePost class="mb-2" @nextEmit="next()" @prevEmit="prev()"
    :inicio="inicio" :fin="fin" :maxLength="maxLength"
  />

  <BlogPost 
    v-for="post in posts.slice(inicio, fin)" 
    :key="post.id" 
    :id="post.id"
    :title="post.title" 
    :subtitle="post.subtitle" 
    :body="post.body" 
    :colorText="post.colorText"
    :cambiarFavorito="cambiarFavorito"
    class="mb-2"
    />

  </div>
</template>