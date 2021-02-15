<template>
  <div id="myDIV" class="header">
    <h2 style="title">My To Do List</h2>

    <span>
      {{ checkFlagList.filter(data=> data).length}} out of {{ dataLength }} items completed
    </span>
    <br>
    <input 
      type="text"
      id="myInput" 
      placeholder="Insert todo List..." 
      v-model="text" 
      @keyup.enter="keyEnter($event)" >

    <button class="addBtn" @click="keyEnter($event)">Add</button>

    <li-component 
      v-for="(data, index) in dataList" 
      :key="index" 
      :propsData="data" 
      @removeClick="deleteList" 
      @checkFlag="checkFun"
      @editSave="editFun" />
  </div>
</template>

<script>
import liComponent from '../components/TheLiComponents.vue';

export default {
  components: {liComponent},
  data() {
    return {
      dataList: [],
      dataLength: 0,
      checkFlagList: [],
      text: '',
    }
  },
  methods: {
    keyEnter(e) {
      if(/^\W/g.test(this.text) || this.text === '') {
        alert('잘좀 하자')
      } else {
        this.dataList.push(this.text);
        this.dataLength = this.dataList.length;
      }
    },
    deleteList(name) {
      const dataList = this.dataList;
      dataList.splice(dataList.indexOf(name), 1);
      this.dataLength = dataList.length;
    },
    editFun(type, text) {
      let i = 0;
      let arr = [];
      for(let value of this.dataList) {
        if(value === type) {
          arr[i] = text;
        } else {
          arr[i] = value;
        }
        i++; 
      }
      this.dataList = [...arr];
    },
    checkFun(flag) {
      const checkFlagList = this.checkFlagList;
      if(flag) {
        checkFlagList.push(flag);
      } else {
        checkFlagList.splice('checkFlagList'.indexOf(false));
      }
    },
    localStorageItems(type = 'get', itemType='', data={}) {
      if(type === 'get') {
          localStorage.getItem(itemType, data);
      } else {
          localStorage.setItem(itemType, data);
      }
    }
  }
}
</script>

<style scoped>

</style>