<template>
  <v-app>
    <v-main>
        <v-app-bar color= "#b4897f"> Usuário
          <v-toolbar-title  class="ml-15">A Rede Social</v-toolbar-title>
          <v-spacer></v-spacer>
          <DeleteAll @delete="apagarPostagens" />
        </v-app-bar>
      
      <div class="postagens-container">
        <div v-for="(post, index) in feed" :key="index">
          <SendPost :postProp="post" @editar-post="editarPost" @excluir-post="excluirPost"/>
          
          <v-dialog v-model="dialogEditar" max-width="600px">
            <v-card>
              <v-card-title>Editar Publicação</v-card-title>
              <v-card-text>
                <v-text-field
                  v-if="postParaEditar"
                  v-model="postParaEditar.text"
                  label="Editar Texto"
                  outlined
                  dense
                ></v-text-field>
              </v-card-text>

              <v-card-actions>
                <v-btn @click="salvarEdicao">Salvar</v-btn>
               <v-btn @click="dialogEditar = false">Cancelar</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>

          </div>
      </div>
      <BottomBar @send-post="addPost"/>

    </v-main>
  </v-app>
</template>

<script>

import SendPost from './components/SendPost.vue'; 
import BottomBar from './components/BottomBar.vue';
import DeleteAll from './components/DeleteAll.vue';

export default {
  name: 'App',

components:{
  SendPost,
  BottomBar,
  DeleteAll
},
  data: () => {
    return {
      dialogEditar: false,
      postParaEditar: null,
      feed:[
        {
          id: '4', 
          name: 'Guilherme', 
          text: 'Boa tarde galera da rede social...', 
          imgperfil: 'https://sujeitoprogramador.com/instareact/fotoPerfil2.png', 
          likeada: true, 
          likers: 32,
          editado: false 
        },
        {
          id: '1', 
          name: 'Lucas Silva', 
          text: 'Mais um dia de muitos bugs :)', 
          imgperfil: 'https://sujeitoprogramador.com/instareact/fotoPerfil1.png', 
          imgPublicacao: 'https://sujeitoprogramador.com/instareact/foto1.png',  
          likeada: true, 
          likers: 1,
          editado: false 
        },
        {
          id: '2', 
          name: 'Jose Augusto', 
          text: 'Bora trabalhar, hoje estou começando em um projeto novo aqui no trabalho, desde o backend ao frontend', 
          imgperfil: 'https://sujeitoprogramador.com/instareact/fotoPerfil3.png', 
          likeada: false, 
          likers: 3,
          editado: false 
        },
        {
          id: '3', 
          name: 'Matheus', 
          text: 'Isso sim é ser raiz!!!!!', 
          imgperfil: 'https://sujeitoprogramador.com/instareact/fotoPerfil2.png', 
          imgPublicacao: 'https://sujeitoprogramador.com/instareact/foto2.png', 
          likeada: false, 
          likers: 0,
          editado: false 
        }
      ]
    }
  },
  methods:{
    addPost(e){
    e.editado = false; // Adiciona a propriedade editado ao novo post
    e.criadoPeloBottomBar = true; // Define criadoPeloBottomBar como true
    this.feed.unshift(e);
  },
  editarPost(post) {
    this.postParaEditar = post;
    this.dialogEditar = true;
  },
  salvarEdicao() {
      this.postParaEditar.editado = true;
      this.dialogEditar = false; 
  },
  apagarPostagens() {
    this.feed = []; 
  },
  excluirPost(post) {
    const index = this.feed.indexOf(post);
      if (index > -1) {
        this.feed.splice(index, 1);
      }
  }
  }
};
</script>
