<template>
  <div class="mensagem" v-bind:class="{verde: verde}">
    {{conteudo}}
    <span>{{horario}}</span>
  </div>

</template>

<script>
export default {
  props : ['conteudo' , 'horario' , 'verde']
}
</script>

<style>
.verde {
  background: rgb(220,248,198) impor !important;
  align-self: flex-end;
}

.mensagem {
  font-size:14px;
  box-shadow: rgba(0,0,0,0.13) 0px 1px 0.5px 0px;
  background: white;
  margin :5px 100px;
  padding :5px 10px;
  border-radius:5px;
  width:fit-content;
}

.mensagem span {
  margin-left:25px;
  font-size:11px;
  color:gray;

}

</style>