  
<template>
   <div >
       <h1>Введите населеный пункт </h1>
       <input v-model="dep" >
       <br><button v-on:click="checkDeps">Знайти відділення</button>
       <br><select>
           <option  v-for="dep in otdel" v-bind:key="dep.CityRef" v-bind:value="dep.Description">{{ dep.Description}}</option>
       </select>
   </div>
</template>

<script>
    import Vue from 'vue'
    import axios from 'axios'
    import VueAxios from 'vue-axios'
 
   export default {
        data: function() {
           return {
           cytyes:[],
           otdel:[],
           dep:"Запоріжжя",
           
        }},
        mounted: function(){
            
                axios.post("https://api.novaposhta.ua/v2.0/json/Address/getCities", {
                        apiKey: "8569bc0d64cca934aa4d2e95b5a659a3",
                        modelName: "Address",
                        calledMethod: "getCities",
                        methodProperties: {}
                })
                .then((response)=>{
                    console.log(response.data);
                    this.cytyes = response.data.data;
                })
                
                
            
        },
        methods:{
            checkDeps: function() {
                
                 axios.post("https://api.novaposhta.ua/v2.0/json/Address/getWarehouses", {
                        apiKey: "8569bc0d64cca934aa4d2e95b5a659a3",
                        modelName: "Address",
                        calledMethod: "getWarehouses",
                        methodProperties: {
                            CityName: this.dep,
                        }
                })
                .then((response)=>{
                    console.log(response.data);
                    this.otdel = response.data.data;
                })
            }
        
        }
    }
</script>
<style scoped>
</style>