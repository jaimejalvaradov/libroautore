<template>
  <div class="app">
    <h1>Gestor de Autores</h1>
    <p class="subtitulo">Prototipo FrontTech · Vue.js</p>

    <label for="buscador">Buscar autor</label>
    <input
      id="buscador"
      v-model="terminoBusqueda"
      placeholder="Ej: García Márquez"
    />

    <p class="contador-destacados">
      ⭐ Autores destacados: <strong>{{ totalDestacados }}</strong>
    </p>

    <p v-if="autoresFiltrados.length === 0" class="estado">
      No se encontraron autores.
    </p>

    <div class="lista">
      <AutorCard
        v-for="autor in autoresFiltrados"
        :key="autor.id"
        :nombre="autor.nombre"
        :bio="autor.bio"
        :cantidad-libros="autor.cantidadLibros"
        :es-destacado="destacados.has(autor.id)"
        @destacar="toggleDestacado(autor.id)"
      />
    </div>
  </div>
</template>

<script>
import AutorCard from './components/AutorCard.vue';
import { autores } from './data/autores.js';

export default {
  name: 'App',
  components: { AutorCard },
  data() {
    return {
      terminoBusqueda: '',
      autores: autores,
      destacados: new Set()
    };
  },
  computed: {
    autoresFiltrados() {
      const termino = this.terminoBusqueda.trim().toLowerCase();
      if (!termino) return this.autores;
      return this.autores.filter((autor) =>
        autor.nombre.toLowerCase().includes(termino)
      );
    },
    totalDestacados() {
      return this.destacados.size;
    }
  },
  methods: {
    toggleDestacado(id) {
      if (this.destacados.has(id)) {
        this.destacados.delete(id);
      } else {
        this.destacados.add(id);
      }
      this.destacados = new Set(this.destacados);
    }
  }
};
</script>

<style>
body {
  font-family: system-ui, sans-serif;
  background: #f5f6f8;
  display: flex;
  justify-content: center;
  padding: 40px 16px;
}
.app {
  background: #fff;
  border-radius: 10px;
  padding: 32px;
  max-width: 480px;
  width: 100%;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
}
h1 { font-size: 20px; margin: 0 0 4px 0; }
.subtitulo { font-size: 13px; color: #888; margin: 0 0 20px 0; }
label { display: block; font-size: 13px; color: #555; margin-bottom: 4px; }
input {
  width: 100%;
  padding: 8px 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
  margin-bottom: 16px;
  box-sizing: border-box;
}
.contador-destacados { font-size: 14px; margin-bottom: 16px; }
.estado { font-size: 13px; color: #888; margin-bottom: 12px; }
.lista { display: flex; flex-direction: column; }
</style>
