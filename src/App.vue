<template>

<div id="app"></div>
<img  class="img" src="./assets/cronometro.png" alt="">
<a class="timer"> {{numero}}</a>


<div class="areaBtn">
  <button class="botao" @click="vai()">{{botao}}</button>
  <button class="botao" @click="limpar()">Limpar</button>
</div>

<div class="list" v-show="historico.length > 0">
  <ul>
    <li v-for="item in historico" :key="item">Pausa feita em: {{item}}</li>
  </ul>
  <button @click="limparHistorico">Limpar historico</button>
</div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      numero: 0,
      botao: "Vai",
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico: []
    }
  },
  methods: {
    vai(){
      if(this.timer !== null){

        clearInterval(this.timer);
        this.timer = null;
        this.botao = "Vai"
        
        if(this.ss !== 0){
          this.historico.push(this.numero)
        }

      }else{
        this.timer = setInterval(() => {
          this.rodarTimer()
        }, 1000)
        this.botao = "Pausar"
      }
    },
    limpar(){

      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null
      }
      this.ss = 0
      this.mm = 0
      this.hh = 0
      this.numero = 0
      this.botao = "Vai"

    },
    rodarTimer(){
      this.ss ++;
      if(this.ss == 59){
        this.ss = 0
        this.mm++;
      }

      if(this.mm == 59){
        this.mm = 0
        this.hh++
      }
      let format = (this.hh < 10 ? '0'+this.hh : this.hh) + ':' + (this.mm < 10 ? '0'+this.mm : this.mm) + ':' +(this.ss < 10 ? '0'+this.ss : this.ss )
                  
      return this.numero = format
    },
    limparHistorico(){
      this.historico = []
    }
  }
}
</script>

<style>
#app{
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.img{
  width: 420px;
  height: 420px;
  padding-top: 100px;
}
.timer{
  color: #fff;
  font-size: 70px;
  margin-top: -210px;
}
.areaBtn{
  margin-top: 155px;
  display: flex;
}
.botao{
  -webkit-user-select: none;
  width: 150px;
  background: #fff;
  font-size: 20px;
  border-radius: 8px;
  text-align: center;
  margin-left: 15px;
  margin-right: 15px;
  padding: 6px;
  cursor: pointer;
  transition: all 0.5s;
}
.botao:hover{
  opacity: 0.7;
}

ul{
  text-align: center;
  padding: 0;
}
ul li{
  list-style: none;
  margin-top: 4px;
  padding: 15px;
  background: rgb(70,70,70);
  color: #fff;
  font-size: 18px;
  border-radius: 8px;
}
.list button{
  cursor: pointer;
  background: #fff;
  padding: 8px;
  border-radius: 8px;
  margin-bottom: 12px;
}
</style>
