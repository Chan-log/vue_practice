<template>
  <div class="header">
    <ul class="header-button-left">
      <li v-if="step==1 || step == 2" @click="step=0">Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step==1" @click="step=2">Next</li>
      <li v-if="step==2" @click="publish">Upload</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container @mainText="contentUpload" :post="post" :step="step" :imageUrl="imageUrl"/>
  <button v-if="step==0" @click="moreData">더 보기</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="uploadImage" accept="image/*" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
</template>

<script>

import Container from './components/Container.vue'
import postData from './assets/postData';
import axios from 'axios'
export default {
  name: "App",
  data(){
    return{
      post : postData,
      pageData : 0,
      step: 0,
      imageUrl: "",
      contentData: "",
    }
  },
  components: {
    Container : Container,
  },
  methods : {
    contentUpload(content){
      this.contentData = content
    },
    publish(){
      var postData = 
      {
      name: "Kim Hyun",
      userImage: "https://placeimg.com/100/100/arch",
      postImage: this.imageUrl,
      likes: 0,
      date: "May 15",
      liked: false,
      content: this.contentData,
      filter: "perpetua"
      };
      this.post.unshift(postData)
      this.step = 0;
    },
    uploadImage(e){
      let file = e.target.files;
      let url = URL.createObjectURL(file[0]);
      this.imageUrl = url;
      this.step=1;
},
    moreData(){
      axios.get("https://codingapple1.github.io/vue/more"+ this.pageData +".json").then(result=>{
        this.post.push(result.data);
        this.pageData++;
      })
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>
