<template>
  <div id="app">
    <AddLineItem v-on:add-line-item="addLineItem" />
    <!-- <LineItemList> component has the prop from its .vue file binded to the data object(variable) LineItemList  -->
    <!-- <LineItemList> component is 'watching for' the del-line-item emitter and executing the delLineItem function when emit is caught (passed from child)  -->
    <LineItemList v-bind:propLineItemList="LineItemList" v-on:del-line-item="delLineItem" />
  </div>
</template>

<script>
import LineItemList from '../components/LineItemList'; //importing LineItemList component
import AddLineItem from '../components/AddLineItem'; //importing AddLineItem component
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    AddLineItem,
    LineItemList
  },
  data(){ //data object containing the data for this application (variables)
    return{
      LineItemList: [  //LineItemList array is declared empty in order to fill it using REST API requests
        /*{
          id: 1,
          title: "List Item 1",
          completed: false
        },
        {
          id: 2,
          title: "List Item 2",
          completed: false
        },
        {
          id: 3,
          title: "List Item 3",
          completed: false
        } */
      ]
    }
  },
  methods: { //method object containing the methods (functions) to run in the 'App' component instance
    delLineItem(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.LineItemList = this.LineItemList.filter(todo => todo.id != id))
      .catch(err => console.log(err));//log error if error is passed

      // line below no longer needed --- was used to delete from the hardcoded array data
      //this.LineItemList = this.LineItemList.filter(todo => todo.id != id); // 
    },
    addLineItem(newItem){
      const { title, completed } = newItem;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title: title,
        completed: completed
      })
      .then(res => this.LineItemList = [...this.LineItemList, res.data])// this line will take the res object and 
      .catch(err => console.log(err));//log error if error is passed

      //  line below no longer needed --- was used to create new LineItem object in array data
      //this.LineItemList = [...this.LineItemList, newItem]; // spread opperator, [... X, Y] will grab all of array X and append Y to it
    }
  },
  created(){  // creaated() will run first when Vue instance is created (it will make a GET API request to fill out array data)
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5') // "?_limit=5" limits the amount of LineItems grabbed to 5
    .then(res => this.LineItemList = res.data)// this line will take the res object and assign its data to the blank LineItemList array
    .catch(err => console.log(err));//log error if error is passed
  }
}
</script>

<style> /* styling IS NOT "scoped", so these CSS styles effect all corrosponding elements */
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.bth:hover{
  background: #666;
}

</style>
