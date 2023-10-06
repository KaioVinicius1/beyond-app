<template>
    <v-main>
      <div class="viewPerfil">
        <img
          :src="postProp.imgperfil"
          class="fotoPerfil"
          :alt="postProp.name"
        />
        <span class="nomeUsuario">{{ postProp.name }}</span>
      </div>

      <img
        v-if="postProp.imgPublicacao"
        :src="postProp.imgPublicacao"
        class="fotoPublicacao"
        alt="Publicação"
      />

      <div class="areaBtn">
        <button @click="mostraLikes">
          <img
            :src="carregaIcone(postProp.likeada)"
            class="iconeLike"
            alt="Curtir"
          />
        </button>

        <button class="btnsend">
          <img
            src="@/assets/comment.png"
            class="iconeLike"
            alt="Comentar"
          />
        </button>

        <button class="btnsend">
          <img
            src="@/assets/send.png"
            class="iconeLike"
            alt="Enviar"
          />
        </button>

        <v-btn v-if="postProp.criadoPeloBottomBar" class="ml-3" color="#d9c4bf" @click="editarPost">
          <v-icon>mdi-pencil</v-icon>
        </v-btn>
        <v-btn  v-if="postProp.criadoPeloBottomBar" class="ml-3" color="#d9c4bf" @click="excluirPost">
          <v-icon>mdi-delete</v-icon>
        </v-btn>

      </div>

      <span v-if="postProp.likers > 0" class="likes">
        {{ mostraLikes() }}
      </span>

      <div class="nomeRodape">{{ postProp.name }}</div>
      <span v-if="postProp.editado" class="editado-indicador">(Editado)</span>
      <div class="descRodape">{{ postProp.text }}</div>

      <div class="proximaPublicacao"></div>

    </v-main>
</template>

<script>
export default {
  name: 'SendPost',

  props: {
    postProp: {
      type: Object,
      required: true
    },
    criadoPeloBottomBar: {
    type: Boolean,
    default: false
  }
  },

  data: () => ({
    likeIcon: ''
  }),

  methods: {
    carregaIcone(likeada) {
  return likeada ? require('@/assets/likeada.png') : require('@/assets/like.png');
},

    mostraLikes() {
      if (this.postProp.likers === 0) {
        return null;
      }

      return `${this.postProp.likers} ${this.postProp.likers > 1 ? 'curtidas' : 'curtida'}`;
    },
    editarPost() {
      this.$emit('editar-post', this.postProp); 
    },
    excluirPost() {
      this.$emit('excluir-post', this.postProp);
    }
  }
};
</script>


<style scoped>
.proximaPublicacao {
  margin-top: 10px; 
  border-top: 1px solid #d9c4bf;
  padding-top: 10px; 
}
.viewPerfil {
  display: flex;
  align-items: center;
  padding: 8px;
}

.fotoPerfil {
  width: 50px;
  height: 50px;
  border-radius: 25px;
}

.nomeUsuario {
  padding-left: 5px;
  font-size: 22px;
  color: #000;
}

.fotoPublicacao {
  height: 400px;
  align-items: center;
  width: 100%;
}

.areaBtn {
  display: flex;
  padding: 5px;
}

.iconeLike {
  width: 25px;
  height: 25px;
}

.btnsend {
  padding-left: 10px;
}

.likes {
  font-weight: bold;
  margin-left: 5px;
}

.nomeRodape {
  font-size: 18px;
  font-weight: bold;
  padding-left: 5px;
}

.descRodape {
  padding-left: 5px;
  padding-bottom: 10px;
  font-size: 15px;
}
</style>