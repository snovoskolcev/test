<template>
  <div id="app">
    <div class="container">
      <div class="container__left">
        <input type="text" v-model="linkImg">
        <button @click="setImage(linkImg)">Ok</button>
      </div>
      <div class="container__right">
        <img :src="showImg.src" alt="picture" v-if="showImg.src">
        <div v-else>Введите ссылку на изображение</div>
      </div>
    </div>
  </div>
</template>

<script lang="js">

export default {
  name: 'App',
  data(){
    return{
      linkImg:"",
      showImg:new Image()
    }
  },
  methods:{
    setImage(link){
      const img = new Image();
      img.onload = function () {
        if(this.height > this.width){
          this.width = this.width/5;
          this.height = this.height/4;
        }
        if(this.width > this.height){
          this.width = this.width/16;
          this.height = this.height/9;
        }
      }
      img.onerror = () => {
        this.showImg = new Image();
        this.linkImg = "";
        alert('Неверно выбранна ссылка!');
      }
      img.src = link;
      this.showImg = img;
    }
  }
}
</script>

<style>
.container{
  display: flex;
  justify-content: center;
  height:50vh;
  width:100%;
}
.container__left{
  flex:1;
}
input{
  width:60%;
}
button{
  width:20%;
}
.container__right{
  flex:1;
  text-align: center;
}
img{
  width: 100%;
  height: 100%;
  object-fit: contain;
}
</style>
