<script setup>
//importando funcion 
//para crear referencias reactivas
import { ref } from 'vue'
// Creando una referencia reactiva
// de tipo string
//expresion retorna un valor
const header = ref('App lista de compras');
const shoppingIcon = ref('material-icons shopping-cart-icon');
//Creando una referencia reactiva
//para almacenar el valor de la lista
const items = ref([
// {id: 0, label:'leche'},
// {id: 1, label:'Arroz'},
// {id: 2, label:'Carne'},
// {id: 3, label:'Pan'},
// {id: 4, label:'Huevos'}
  ]);
  const newItem = ref('');
  const newItemHighPriority = ref(false);
  // Metodos
  const saveItems = () =>{
   items.value.push({ id:items.length, label: newItem.value})
  //  Borrar el contenido de la caja de texto
  newItem.value="";
  };
  const editing = ref (false);
  const doEdit = (edit) =>{
    editing.value = edit,
    newItem.value ="";
  }

</script>

<template>
  <!-- Header -->
  <div>
  <h1>
    <i :class="shoppingIcon">local_mall</i> {{ header }} 
  </h1>
  <button class="btn" v-if="editing" v-on:click="doEdit(false)">Cancelar</button>
  <button class="btn btn-primary" v-if="!editing" v-on:click="doEdit(true)">Agregar articulos</button>
</div>
  <!-- Formulario -->
  <form 
  v-if="editing"
  v-on:submit.prevent="saveItems" class="add-item form">
  <input 
  v-model="newItem" type="text"
  placeholder="Agregar articulo">
  <!-- boton -->
  <label ><input type="checkbox" v-model="newItemHighPriority">Alta prioridad</label>
  <button class="btn btn-primary">Agregar articulo</button>
  </form>
  <!-- Entrega de lista -->
  <ul>
    <li v-for="{id, label} in items" v-bind:key="id">⭐{{ label }}</li>
  </ul>
  <!-- Mensaje condicional -->
  <p v-if="items.length === 0">🥀No hay elementos en la lista🥀</p>
</template>

<style scoped>
.shopping-cart-icon{
  font-size: 2rem;
}
</style>
