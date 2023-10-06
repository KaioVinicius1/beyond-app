<template>
    <v-btn rounded @click="$emit('delete')"> <!-- Emitindo evento 'delete' -->
      <v-icon color="#d9c4bf">mdi-delete-forever</v-icon>
    </v-btn>
  </template>
  
  <script>
  export default {
    name: 'DeleteAll'
  }
  </script>
  