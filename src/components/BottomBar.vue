<template>
  <v-main class="postagens-container">
    <v-app-bar fixed bottom color= "#c6a69f">
      <v-text-field v-model="textInput" @keyup.enter="sendPost()" solo hide-details label="fale algo para o mundo"></v-text-field>
      <v-btn @click="sendPost()" icon color="#ffffff">
            <v-icon>mdi-send</v-icon>
          </v-btn>
        </v-app-bar>
  </v-main>
</template>

<script>
  export default {
    name: 'BottomBar',
    
    data(){
      return{
        textInput: '',
      }
    },
    methods:{
    sendPost(){
      let post = {
        name: "Usuário",
        text: this.textInput, 
        imgperfil: require('@/assets/usuario.png')
      }
      this.$emit('send-post', { ...post, criadoPeloBottomBar: true });
      this.textInput = ''
      }
    }
  }
</script>

<style scoped>
.postagens-container {
  margin-bottom: 64px; 
}
</style>
