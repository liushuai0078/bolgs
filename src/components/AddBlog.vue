<template>
  <div id="add-blog">
    <h1 class="center">添加博客</h1>
    <form action="" v-if="!submited">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required>

      <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>

      <div id="checkboxes">
        <label>Vue.js</label>
        <input type="checkbox" value="Vue.js" v-model="blog.categories">
        <label>node.js</label>
        <input type="checkbox" value="node.js" v-model="blog.categories">
        <label>react.js</label>
        <input type="checkbox" value="react.js" v-model="blog.categories">
        <label>angular.js</label>
        <input type="checkbox" value="angular.js" v-model="blog.categories">
      </div>
      <label>作者:</label>
      <select v-model="blog.author">
        <option v-for="author in authors" :key="author" >{{author}}</option>
      </select>
      <button @click.prevent="post">添加博客</button>
    </form>


    <div v-if="submited">
      <h3>您的博客发布成功</h3>
    </div>
    <div id="preview">
      <h3>博客总览</h3>
      <p>博客标题:{{blog.title}}</p>
      <p>博客内容:</p>
      <p>{{blog.content}}</p>

      <p>博客分类:</p>
      <ul>
        <li v-for="category in blog.categories" :key="category">
          {{category}}
        </li>
      </ul>
      <p>作者:{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  // https://jsonplaceholder.typicode.com/
  // https://jsonplaceholder.typicode.com/posts
  name: 'add-blog',
  data(){
    return {
      blog:{
        title:'',
        content:'',
        categories:[],
        author:''
      },
      authors:['hemia','henry','bucky'],
      submited:false
    }
  },
  methods:{
    post(){
      // var _this = this;
      // this.$http.post("https://wd9086734151cepuuy.wilddogio.com/posts.json",this.blog)
      axios.post("/posts.json",this.blog)
      
      .then((data) =>{
        console.log(data);
        // _this.submited = true;
        this.submited = true;
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog{
    box-sizing:border-box;
}
#add-blog{
    margin:20px auto;
    max-width: 600px;
    padding:20px;
}
.center{
  text-align: center
}
label{
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],textarea,select{
  display: block;
  width:100%;
  padding:8px;
}
textarea{
  height:200px;
}
#checkboxes label{
  display: inline-block;
  margin-top:0;
}
#checkboxes input{
  display: inline-block;
  margin-right:10px;
}
button{
  display: block;
  margin:20px 0;
  background:crimson;
  color:#fff;
  padding:14px;
  border-radius: 4px;
  font-size:18px;
  cursor: pointer;
}
#preview{
  padding:10px 20px;
  border:1px dotted #ccc;
  margin:30px 0;
}
h3{
  margin-top:10px;
}
</style>
