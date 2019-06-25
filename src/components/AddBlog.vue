<template>
  <div id="add-blog">
   <h2>添加博客</h2>
   <form v-if="!submmited">
      <label>博客标题</label>
      <input type="text" v-model="blog.title" required />

       <label>博客内容</label>
      <textarea v-model="blog.content"></textarea>

      <div id="checkboxes">
        <label>Vue.js</label>
        <input type="checkbox" value="Vue.js" v-model="blog.categories">
         <label>Node.js</label>
        <input type="checkbox" value="Node.js" v-model="blog.categories">
         <label>React.js</label>
        <input type="checkbox" value="React.js" v-model="blog.categories">
         <label>Angular4</label>
        <input type="checkbox" value="Angular4" v-model="blog.categories">

      </div>
      <label>作者：</label>
      <select v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
      <button v-on:click.prevent="post">添加博客</button>
   </form>
   
   <div v-if="submmited">
     <h3>您的博客发布成功！</h3>
   </div>

  <div id="preview">
    <h3>博客总览</h3>
    <p>博客标题：{{blog.title}}</p>
    <p>博客内容：{{blog.content}}</p>
    <p>博客分类：</p>
     <ul>
      <li v-for="category in blog.categories">{{category}}</li>
    </ul>
    <p>作者：{{blog.author}}</p> 
  </div>

  </div>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'add-blog',
  data () {
    return {
      blog:{
        title:"",
        content:"",
        categories:[],
        author:""
      },
      authors:["Mike","Henry","Luncy"],
      submmited:false
    }
  },
  methods:{
    post:function(){
      // this.$http.post("https://vuedemo-d6270.firebaseio.com/posts.json",this.blog)
      //  var _this=this; 方法一
      // axios.post("https://vuedemo-d6270.firebaseio.com/posts.json",this.blog)
      // .then(function(data){
      //     console.log(data);
      //     _this.submmited = true;
      // });


//方法二（推荐）
      axios.post("/posts.json",this.blog)
      .then((data)=>{  //ES6语法
          // console.log(data);
          this.submmited = true;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog *{
  box-sizing: border-box; 
}

#add-blog{
  margin:20px auto;
  max-width:600px;
  padding: 20px;
}

label{
  display: block;
  margin:20px 0 10px;
}

input[type="text"],textarea,select{
  display: block;
  width: 100%;
  padding: 8px;
}

textarea{
height: 200px;
}

#checkboxes label{
  display: inline-block;
  margin-top: 0;
}
#checkboxes input{
  display: inline-block;
  margin-right:10px;
}
button{
  display: block;
  margin-top: 20px;
  background: crimson;
  color: #fff;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor:pointer;
}

#preview{
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin:30px 0;
}

h3{
  margin-top: 10px;
}
</style>
