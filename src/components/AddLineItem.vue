<template>
    <div>
        <form @submit.prevent="addLineItem"> 
            <!--- ".prevent" on @submit to prevent page reloading and submitting info to file 
                @submit will also execute the addLineItem method --->
            <!--- text input field uses v-model to tie the input to the data variable "text" --->
            <input type="text" v-model="title" name="title" placeholder="Add Todo" >
            <!--- Submit button --->
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
//import uuid from 'uuid'; //inporting UUID library for creating unique ids -- not needed with API

export default {
    name: "AddLineItem",
    data(){
        return{
            title: ''
        }
    },
    methods:{
        addLineItem(){
            const newLineItem = { //declaring a new LineItem object
                //id: uuid.v4(), //give new LineItem a unique ID using UUID library ---- only need this if database/API does auto assign ID
                title: this.title, //the LineItem title is set to the data variable "title"
                completed: false  //automatically sets the completed field to "False" for new LineItems
            }
            //send new LineItem object up to parent
            this.$emit('add-line-item', newLineItem);
            this.title = ''; //this will clear the textbox input when submitted
        }
    }
}
</script>

<style scoped>
form{
    display: flex;
}

input[type="text"]{
    flex: 10;
    padding: 5px;
}

input[type="submit"]{
    flex: 2;
}

</style>