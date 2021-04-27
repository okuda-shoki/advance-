<template>
  <div class="home">
    <div class="home_content">
     <h1 class="todo">Todo<span class="padding">List</span></h1>
     <div class="add flex">
       <input type="text" v-model="text"
       class="sendtext"/>
       <button @click="send()" class="submit-button button">追加</button>
       </div>
       </div>
     <table  class="advance_table" v-for="data in list" :key="data.id">
       <tr class="advance_tr">
         <td><input type="text" v-model="data.name" class="text_space"/></td>
         <div class="button_drive">
         <button @click="updb(data.id,data.name)" class="update_button button">更新</button>
         <button @click="delb(data.id)" class="delete_button button">削除</button>
         </div>
       </tr>
     </table>
     </div>
</template>

<script>
import axios from "axios";
export default {
  created(){
    this.getContact()
  },
  data(){
    return{
      text:"",
      list:[],
    };
  },
  methods:{
    async getContact(){
      const resData=await axios.get("http://127.0.0.1:8000/api/test/");
      this.list=resData.data.data;
    },
    async send(){
      const sendData={
        name:this.text
      };
    await axios.post("http://127.0.0.1:8000/api/test/",sendData);
    await this.getContact();
    this.text=""
    },
    async updb(id,name) {
      const sendData = {
        name: name,
      };
      await axios.put("http://127.0.0.1:8000/api/test/"+id, sendData);
      await this.getContact();
    },
    async delb(id) {
      await axios.delete("http://127.0.0.1:8000/api/test/" + id);
      await this.getContact();
    },
  },
};
</script>

<style scoped>

.flex{
  display: flex;
  justify-content: space-between;
}

.button{
  padding: 10px 15px;
  background-color: #fff;
  cursor: pointer;
  border-radius: 10px;
}

.home{
  border: 1px solid #fff;
  border-radius: 10px;
  background-color: #fff;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}

.home_content{
  padding:30px 30px 20px 30px;
}

.home h1{
  text-align: left;
  font-size: 25px;
  font-weight: bold;
}

.add{
  width: 50vw;
  margin-top:15px;
  box-sizing: border-box;
}

.padding{
  margin-left: 10px;
}

.sendtext{
  width: 80%;
  border: 1px solid #ccc;
  padding: 15px;
}

.submit-button{
  color: #dc70fa;
  border: 3px solid #dc70fa;
  margin-left: 30px;
}

.submit-button:hover{
  background-color: #dc70fa;
  color: #fff;
  transition: 0.7s;
}

.advance_table{
  display: inline-block;
  margin-bottom: 25px;
  width: 50vw;
}

.advance_tr{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.text_space{
   border: 1px solid #ccc;
   width: 100%;
   padding: 15px;
}

.update_button{
  color: #fa9770;
  border: 3px solid #fa9770;
}

.update_button:hover{
  background-color:#fa9770 ;
  color: #fff;
  transition: 0.7s;
}

.delete_button{
  color: #71fadc;
  border: 3px solid #71fadc;
  margin-left: 10px;
}

.delete_button:hover{
  background-color:#71fadc;
  color: #fff;
  transition: 0.7s;
}
</style>