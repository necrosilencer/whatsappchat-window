<template>
  <div>
    <section class="section">
      <div class="container">
        <div class="columns">
          <div class="column is-3 lista-de-conversas" >
            <div class="barra-superior"></div>
              <div class="item" v-for='(conversa,index) in conversas' :key="index"
              @click="indiceAtivo = index">
                <div class="title is-6">
                    {{conversa.usuario}}
                </div>
                <div class="subtitle is-6">
                  Ultima mensagem...
                </div>
              </div>
          </div>
          <div class="column conversa-ativa">
            <div class="barra-superior">
              <span>{{conversas[indiceAtivo].usuario}}</span>
            </div>
            <div class="lista-mensagens">
            <Mensagem
              v-for="(mensagem,indice) in conversas[indiceAtivo].mensagens"
              :key="indice"
              :conteudo="mensagem.conteudo"
              :horario="mensagem.horario"
              :verde="mensagem.verde"
            />
            </div>
            <div class="barra-inferior">
              <input v-model="conteudoNovaMensagem" type="text" class="input" placeholder="Insira a mensagem" v-on:keyup.enter="enviarMensagem">
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import conversasIniciais from './dados.js'
import Mensagem from './mensagem.vue'
export default {
  data: function(){
    return {
      conversas: conversasIniciais,
      indiceAtivo : 0,
      conteudoNovaMensagem : ''
    }
  },
  components: {
    Mensagem
  },
  methods : {
    enviarMensagem : function(){
      let horarioAtual = new Date().getHours() + ':' + new Date().getMinutes();

      let novaMensagem = {
        horario : horarioAtual,
        conteudo: this.conteudoNovaMensagem,
        verde:true,
      };

      this.conversas[this.indiceAtivo]
      .mensagens
      .push(novaMensagem);

      this.conteudoNovaMensagem = "";
    }
  }
}
</script>
<style>

.lista-mensagens{
  height:85%;
  display:flex;
  justify-content: flex-end;
  flex-direction: column;
}


.columns {
  min-height:750px;
  box-shadow : 0 3rem 3rem -1rem rgba(10,10,10,.2);
}

.column {
  padding : 0 ;

}

.lista-de-conversas {
  background:white;

}

.conversa-ativa {
  background:#E5DDD5;
}

.barra-superior {
  margin : 0 ;
  height: 50px;
  background : #EDEDED;
  border-right: 1px solid #e1e1e1;
  border-bottom : 1px solid rgb(200,200,200);
} 

.barra-superior span {
  line-height:50px;
  margin-left:25px;
  font-weight:500;
}

.item {
  border-bottom:1px solid #f2f2f2;
  padding :15px 30px;
  margin-bottom : 0 !important;
}

.subtitle {
  color:gray
}

.item:hover {
  background :#f5f5f5;
  cursor :pointer;
}

.barra-inferior{
  bottom:0;
  width:77%;
  padding:10px;
  position:absolute;
  background:#f0f0f0;
}

.barra-inferior input {
  border:none;
  padding:10px;
  margin : 0 50px;
  width:90%;
  border-radius : 15px;
  font-size:16px;
}

</style>