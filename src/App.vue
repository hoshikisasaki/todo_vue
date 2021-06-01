<template>
  <div id="app">
   <div class="container">
     <div class="card">
       <p class="title mb-15">Todo List</p>
       <div class="todo">
         <div class="mb-15 flex between">
           <input placeholder="新規todoを入力してください" type="text" v-model="newTodo" class="input_add"/>
           <button class="btn_add" @click="insertTodos">追加</button>
         </div>
         <div class="mb-5 flex between" v-for="item in todos" :key="item.id">
           <input type="text" class="input_update" v-model="item.todo"/>
           <div>
           <button class="btn_update" @click="updateTodos(item.id,item.todo)">更新</button>
           <button class="btn_destroy" @click="deleteTodos(item.id)">削除</button>
           </div>
         </div>
       </div>
     </div>
   </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data(){
    return{
      newTodo:"",
      todos:[]
    };
  },
 
    created (){
 this.getTodos();
   },
  methods: {
    async getTodos() {
      const resData = await axios.get("http://127.0.0.1:8000/api/todos/");
      this.todos = resData.data.data;
    },
    async insertTodos() {
      await axios.post("http://127.0.0.1:8000/api/todos/", 
      {
        todo:this.newTodo
      });
      await this.getTodos();
    },
     async updateTodos(id,newTodo) {
     
      await axios.put("http://127.0.0.1:8000/api/todos/" + id, 
      {
        todo:newTodo
      });
      await this.getTodos();
    },
    async deleteTodos(id) {
      await axios.delete("http://127.0.0.1:8000/api/todos/" + id);
      await this.getTodos();
    },
    
   }
  }
 
</script>


<style>
/* リセットcss */

html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

body {
    line-height:1;
}
article,aside,details,figcaption,figure,
footer,header,hgroup,menu,nav,section {
    display:block;
}

nav ul {
    list-style:none;
}

blockquote, q {
    quotes:none;
}

blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}

a {
    margin:0;
    padding:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}

/* change colours to suit your needs */
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}

/* change colours to suit your needs */
mark {
    background-color:#ff9;
    color:#000;
    font-style:italic;
    font-weight:bold;
}

del {
    text-decoration: line-through;
}

abbr[title], dfn[title] {
    border-bottom:1px dotted;
    cursor:help;
}

table {
    border-collapse:collapse;
    border-spacing:0;
}

/* change border colour to suit your needs */
hr {
    display:block;
    height:1px;
    border:0;  
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}

input, select {
    vertical-align:middle;
}

html {
  background-color: #15202b;
}
* {
  color: white;
  font-family: "Noto Sans JP";
}
#app {
background-color: #2d197c;
widows: 100vw;
height: 100vh;
}
.container{
  width: 100%;
  height: 100%;
}
.card{
    background-color: #fff;
    width: 50vw;
    padding: 30px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 10px;
}
.title{
  font-weight: bold;
  font-size: 24px;
  color: black;
}

.input_add{
    width: 80%;
    padding: 5px;
    border-radius: 5px;
    border: 1px solid #ccc;
    appearance: none;
    font-size: 14px;
    outline: none;
    color: black;
}
.input_update{
  width: 30%;
    padding: 5px;
    border-radius: 5px;
    border: 1px solid #ccc;
    appearance: none;
    font-size: 14px;
    outline: none;
    color: black;
}
.btn_add{
    text-align: left;
    border: 2px solid #dc70fa;
    font-size: 12px;
    color: #dc70fa;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
}
.btn_add:hover{
  background-color: #dc70fa;
  color: white;
}
.btn_update{
    text-align: left;
    border: 2px solid #fa9770;
    font-size: 12px;
    color: #fa9770;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
    margin-right: 5px;
}

.btn_update:hover{
  background-color: #fa9770;
  color:white;
}
.btn_destroy{
  text-align: left;
    border: 2px solid #71fadc;
    font-size: 12px;
    color: #71fadc;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
  
}
.btn_destroy:hover{
  background-color: #71fadc;
  color: white;
}

.mb-15{
  margin-bottom: 15px;
}

.mb-5{
  margin-bottom: 5px;
}
.between{
  justify-content: space-between;
}
.flex{
  display: flex;
}

.ff{
  color: #000;
   width: 30%;
    padding: 5px;
    border-radius: 5px;
    border: 1px solid #ccc;
    appearance: none;
    font-size: 14px;
    outline: none;
}

</style>
