<template>
  <div class="home">
 <div v-if="entities.length==0" class="noItems">
        No Items Found
      </div>
    <div v-for="(entity,entityIndex) in entities" v-bind:key="entityIndex" class="_Box">
         
      <div class="mainBoxContent input">
        <h4>
          <span @click="showNameInput = true;currentEntityId = entityIndex;" >
            {{ entity.name }}
          </span>
          <button class="deleteBox" @click="entities.splice(entityIndex,1)" >Romove Item</button>
        </h4>
        <div v-if="updateBtn && showNameInput && currentEntityId == entityIndex">
          <input v-model="entities[entityIndex].name"/>
          <button class="updateButton" @click="toggleInput"> update</button>
         </div>
        <div>
          <h6><button @click="entities[entityIndex].attributes.push({name: 'New Attribute'});showEntityAttributeInput=false" class="addButton">+</button></button> Add New Attribute </h6>
          <ul>
            <li v-for="(entityAttribute,entityAttributeIndex) in entity.attributes">
              <span @click="showEntityAttributeInput=true;entityAttributeInputIndex=entityAttributeIndex" >
                {{ entityAttribute.name }}
              </span>
              <div class="btnGroup">
                <button @click="entities[entityIndex].attributes.splice(entityAttributeIndex,1)"class="dropButton" >-</button>
              
              </div>
              <div v-if="showEntityAttributeInput && entityAttributeInputIndex == entityAttributeIndex" >
                <div v-if="updateBtn">
                  <input v-model="entities[entityIndex].attributes[entityAttributeIndex].name" />
                  <button class="updateButton" @click="toggleInput"> update</button>
                </div>
              </div>
            </li>
            <li title="Double click to edit" v-if="entity.attributes.length == 0" @click="entities[entityIndex].attributes.push({name: 'New Attribute'});showEntityAttributeInput=false" >
              New Attribute
            </li>
          </ul>
        </div>
      </div>
    </div> 
    <div @click="entities.push({attributes: [],name: 'new entity'});showNameInput = false;currentEntityId = null;showEntityAttributeInput=false" class="_ButtonAdd">+</div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'home',
  data() {
    return {
      entities: [],
      showNameInput: false,
      currentEntityId: null,
      showEntityAttributeInput: false,
      entityAttributeInputIndex: null,
      updateBtn: true,
    }
  },
  methods :{
    toggleInput(){
      this.showNameInput = false;
      this.currentEntityId = null;
      this.showEntityAttributeInput = false;
      this.entityAttributeInputIndex = null;
      this.updateBtn= true;
    }
  }
});
</script>

<style>
body{
  position: relative;
  background: #f5f5f5;
  text-align: center;
  margin:auto;
}
.mainBoxContent{
  position: relative;
}
.mainBoxContent h4 span{
  font-size: 20px;
}
.mainBoxContent h4{
  text-transform: capitalize;
}
.mainBoxContent h2{
  margin-bottom: 20px;
}
.mainBoxContent input{
  border-radius: 12px;
  box-shadow: none;
  border: 1px solid #17d3ff;
  outline: none;
      position: absolute;
    top: 18px;
    left: 0;
}

ul li{
      position: relative;
    padding: 8px;
    list-style-type: none;
    background: #f1f1f1;
    padding-left: 6px;
    margin-bottom: 5px;
    border-radius: 5px;
  
}
ul li .dropButton{
  color:red;
  border-radius: 50%;
  border: 0;
  background:transparent;
  font-size: 20px;
  font-weight: 900;
  outline: none;
  box-shadow: none;
}
ul li .addButton{
  background:transparent;
  font-size: 20px;
  font-weight: 900;
  outline: none;
  box-shadow: none;
  color:#17d3ff;
  border-radius: 50%;
  border: 0;
  position: relative;
  
}

ul{
  padding:0;
  overflow-x: hidden;
  overflow-y: auto;
  height:200px;
}
ul li .btnGroup{
  position: absolute;
  right: 0;
  top: 0;
  border-radius: 0px 5px 5px 0px;
    padding: 4px 3px;
}
._Box{
  position: relative;
      height: 400px;
      overflow:hidden;
      text-align: left;
    background: white;
    width: 20%;
    padding: 50px;
    border-radius: 20px;
    margin: 10px;
    box-shadow: 1px 1px 10px #dadada;
        display: inline-block;
}
._ButtonAdd{
  display: block;
  margin:auto;
      padding: 11px 16px;
    background: #17d4ff;
    width: fit-content;
    border-radius: 50%;
    cursor: pointer;
    color: white;
    font-weight: 700;
    text-align: center;
    margin-top: 30px;
    position: fixed;
    left: 0;
    top: 0;
    padding: 14px 20px;
    border-radius: 0px 50% 50% 0px;



}
.updateButton{
      position: absolute;
    right: 0;
    top: 10px;
    background: transparent;
    border: none;
    color: green;
    text-transform: capitalize;
    outline: none;
    box-shadow: none;
    cursor: pointer;
}
input{
    height:30px;
    border-radius:5px !important;
    top: 0 !important;
        width: 100%;
        padding-left: 10px;
  }
.deleteBox{
  position: absolute;
    top: -42px;
    right: 0;
    background: red;
    padding: 4px 24px;
    border-radius: 5px;
    border: none;
    color: white;
    font-size: 14px;
    box-shadow: none;
    outline: none;
    cursor: pointer;
}
.addButton{
      background: #17d3ff;
    border: none;
    outline: none;
    box-shadow: none;
    color: white;
    padding: 2px 8px 3px 8px;
    border-radius: 5px;
    font-size: 13px;
    font-weight: 800;
     margin-right: 5px;
     cursor: pointer;
}
h6{
      font-size: 14px;
   
}
.noItems{
      font-size: 30px;
    color: #b7b7b7;
    position: relative;
    top: 16rem;
    left: 0;
    right: 0;
}
</style>

