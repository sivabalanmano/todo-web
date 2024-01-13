<template>
<div class="flex justify-center items-center p-5">
    <div class="h-[100px] w-[250px] flex justify-center items-center bg-gray-600 drop-shadow-xl p-10 rounded-lg">
        
        <div class=" items-center justify-center rounded-sm">
            <h1  class="flex font-bold justify-center items-center">ToDo App</h1>
           
            <input v-model="Text" 
            class="rounded-sm p-1 " type="text"  
            placeholder="please enter the task"
            @keypress.enter="addtext(index)"
            >

           
        </div>
    </div>
</div>
<div v-for="(total,index) in totalText" 
            :key="index" 
            class="flex justify-center items-center gap-4 ">
            
            <input @change="updateText(index)" type="checkbox">
            <p class="cursor-pointer font-bold" 
            @dblclick="removeText(index)"
            :class="{'line-through' : total.isComplet}" 
            
            >
            {{ total.data }}

            </p>
    </div>
</template>
<script>
   export default {
    data(){
        return{
            Text:"",
            totalText:[
            ]
        }
    },
    methods:{
        getApi(){
           this.$http.$get("/user").then((res)=>{
            this.totalText =res.users;
           })
        },
        addtext(){
            if (this.Text == "") {
                alert("please enter the value")

            }
            else{
                this.$http.$post("/user/add",{
                   body:{
                     data:this.Text,
                   }
                })
                .then((res)=>{
                    this.getApi();
                
                })
                this.totalText = "";
                }
                
            },
            updateText(index){
               this.$http.$patch(`user/update/${ this.totalText[index].id} `, {
                body:{
                    data:this.totalText[index].data,
                    isComplet: !this.totalText[index].isComplet,
                }
               })
               .then((res)=>{
                    this.getApi();
                
                })
            },
            removeText(index){
                this.$http.$delete("/user/delete/" + this.totalText[index].id)
                .then((res)=>{
                    this.getApi();
                
                })
            }
            
        },
    mounted(){
        this.getApi()
    },


}

</script>