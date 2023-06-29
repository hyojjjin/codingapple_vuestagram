<template>
<div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step !=2" @click="onClickNext">Next</li>
      <li v-if="step===2" @click="onClickPublish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container :postData="postData" :step="step" :uploadFileUrl="uploadFileUrl" @writeContent="writeContent" />

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" multiple type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
 </div>

  <!-- ##탭 만들기 연습
     <div>{{this.tapMassages[this.step]}}</div>
    <button @click="onClickBtn0">버튼0</button>
    <button @click="onClickBtn1">버튼1</button>
    <button @click="onClickBtn2">버튼2</button> -->
</template>
 
<script>
import Container from './components/Container.vue';
import PostData from './js/postData.js'

export default {
  name: 'App',
  components: {
    Container : Container
  },
  data() {
    return {
      postData : PostData,
      step : 0,
      uploadFileUrl : '',
      newPostContent : ''
      // step : 0, ##탭 만들기 연습
      // tapMassages : ['내용0', '내용1', '내용2'], ##탭 만들기 연습
    }
  },
  methods : {
    upload(e) {
      let file = e.target.files
      this.uploadFileUrl = URL.createObjectURL(file[0])
      this.step++;
    },
    onClickNext(){
      this.step++
    },
    onClickPublish(){
      var newPost = {      
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.uploadFileUrl,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.newPostContent,
        filter: "perpetua"
      };
      this.postData.unshift(newPost);
      this.step = 0;
    },
    writeContent(e) {
      this.newPostContent = e
    },
    mounted() {
      this.emitter.on('작명', (a) => {
        console.log(a)
      })
    }
    /* ##탭 만들기 연습
      onClickBtn0() {
        this.step = 0
      },
      onClickBtn1() {
        this.step = 1
      },
      onClickBtn2() {
        this.step = 2
      },
    */
  }

}
</script>

<style>
 
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
