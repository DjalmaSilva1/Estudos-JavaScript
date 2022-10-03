<template>
  <div class="container">
      <h1>Comentarios</h1>
      <hr/>
      <div class="form-todo form-group">
        <p>
          <input placeholder="nome" type="text" name="author"
          class="form-control" v-model="name"/>
        </p>
        <p>
          <textarea name="message" placeholder="Comentário" 
          class="form-control" v-model="message"></textarea>
        </p>
        <button @click="addComment" type="submit" class="btn btn-primary" >Comentar</button>
      </div>
    
      <div class="list-group">
        <div class="list-group-item" v-for="(comment, index) in allComments" :key="index">
          <span class="comment_author">Autor: <strong>{{comment.name}}</strong>
          </span>
          <p>{{comment.message}}</p>
          <div>
            <a @click.prevent="removeComment(index)" href="#" title="excluir">Excluir</a>
          </div>
        </div>
      </div>
      <hr/>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      comments: [],
          name: '',
          message: '',
        
   }
  },
  //Evento do botão Comentar
  methods: {
    addComment() {
      if(this.message.trim() === '') {
        alert('Por favor escreva o Comentário...');
        return;
      }

      this.comments.push({
        name: this.name,
        message: this.message,
      });

      //Limpa os Campos dos inputs
      this.name = '',
      this.message = ''
    },

    removeComment(index) {
      this.comments.splice(index, 1);
    }

  },
  //Deixa o Autor anónimo
  computed: {
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anónimo' : comment.name
      }))
    }
  }
}
</script>

<style>

</style>