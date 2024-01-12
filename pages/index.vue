<template>
<div class="flex justify-center items-center p-5">
    <div class="h-[100px] w-[250px] flex justify-center items-center bg-gray-600 drop-shadow-xl p-10 rounded-lg">
        
        <div class=" items-center justify-center rounded-sm">
            <h1  class="flex font-bold justify-center items-center">ToDo App</h1>
           
            <input v-model="Text" 
            class="rounded-sm " type="text"  
            placeholder="please enter the task"
            @keypress.enter="addtext()"
            >

            
        </div>
    </div>
</div>
<div v-for="(total,index) in totalText" 
            :key="index" 
            class="flex justify-center items-center gap-2 ">
            
            <input @change="Text.isComplet = !Text.isComplet" type="checkbox">
            <p class="cursor-pointer font-bold" 
            @dblclick="removeText(index)"
            :class="{'line-through' : Text.isComplet}"
            >
            {{ total.value }}
            </p>
    </div>
</template>
<script>
   export default {
    data(){
        return{
            Text:"",
            totalText:[]
        }
    },
    methods:{
        addtext(){
            if (this.Text == "") {
                alert("please enter the value")

            }
            else{
                this.totalText.push({
                    value:this.Text,
                    isComplet:false
                })
                this.Text == "";
            }
        },
        removeText(index){
            this.totalText.splice(index, 1)
        }
    }
}

</script>