<template>
  <div class="tarjeta-autor" :class="{ destacado: esDestacado }">
    <p class="nombre">{{ nombre }}</p>
    <p class="bio">{{ bio }}</p>
    <p class="cantidad">{{ cantidadLibros }} libros publicados</p>

    <button class="btn-destacar" @click="$emit('destacar')">
      {{ esDestacado ? '★ Destacado' : '☆ Destacar autor' }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'AutorCard',
  props: {
    nombre: { type: String, required: true },
    bio: { type: String, default: '' },
    cantidadLibros: { type: Number, default: 0 },
    esDestacado: { type: Boolean, default: false }
  },
  emits: ['destacar']
};
</script>

<style scoped>
.tarjeta-autor {
  background: #fafafa;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
}
.tarjeta-autor.destacado {
  border-color: #f5c518;
  background: #fffdf5;
}
.nombre { font-weight: 600; margin: 0 0 6px 0; font-size: 15px; }
.bio { margin: 0 0 6px 0; font-size: 13px; color: #555; }
.cantidad { margin: 0 0 10px 0; font-size: 12px; color: #888; }
.btn-destacar {
  background: #eee;
  color: #333;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 13px;
}
.tarjeta-autor.destacado .btn-destacar {
  background: #f5c518;
  color: #333;
}
</style>
