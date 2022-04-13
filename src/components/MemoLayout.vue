<template>
  <div class="memo">
    <div class="act">
    <button class="btn btn-primary" @click="add()">+추가</button>
    </div>
    <ul>
      <li v-for="(d, idx) in state.data" :key="d" @click="edit(idx)">{{d.content}}<button class="btn btn-primary" @click="deleted(idx)">-삭제</button> </li>
    </ul>
  </div>
</template>

<script>
import {  reactive } from "@vue/runtime-core";
import axios from "axios";

export  default {


  setup() {
    const state = reactive({
      data:[]
    })

    const add = ()=>{
      const content = prompt("내용을 입력하세요");
     // state.data.push("추가된 메모 내용")
      axios.post("http://localhost:8080/api/connectTest",{content}).then((response) =>{
        state.data = response.data;
      })
    };


    const deleted = (idx)=>{

      axios.delete("http://localhost:8080/api/connectTest/"+idx,state.data[idx]).then((response) =>{
        state.data = response.data;

      })

    };


    const edit = (idx)=>{
      const content = prompt("내용을 입력하세요", state.data[idx].content);
      state.data[idx].content = content;

      axios.put("http://localhost:8080/api/connectTest/"+idx,state.data[idx]).then((response) =>{
        state.data = response.data;

      })

    };

    axios.get("http://localhost:8080/api/connectTest").then((response) => {
      console.log(response.data)
      state.data = response.data;
    });

    return {state, add, edit, deleted};
  },




};
</script>

<style lang="scss" scoped>
.memo {
  .act {
    padding: 10px 5px 5px 5px;
    text-align: right;
  }
  ul{
    border-top:1px solid aqua;
  list-style:none;
  padding: 0;
  margin: 0;

  li {
    padding: 15px;
    margin: 5px;
  }}
}


</style>