<template>
    <div>
        <!-- <div> element has has a loop displaying all instances of <LineItem> components in the prop array "propLineItemList". 
            "propLineItemList" is passed down from App.vue, where it is "binded" to the variable "LineItemList" -->
        <div v-bind:key="item.id" v-for="item in propLineItemList">

            <!-- <LineItem> component creates a prop "propLineItem" for each "item" in the array "propLineItemList" (declared in above div).
                <LineItem> component is also 'watching for' the del-line-item emitter and is emitting the ID of the corrosponding line item's ID up to parent -->
            <LineItem v-bind:propLineItem="item" v-on:del-line-item="$emit('del-line-item', item.id)"/>
            
        </div>
    </div>
</template>

<script>
import LineItem from './LineItem'; //importing LineItem component

export default {
    name: "LineItemList",
    components: {
        LineItem
    },
    props:{ //prop opject that is binded to the data object "LineItemList" array in parent component Home.vue
        propLineItemList: Array
    }
    
}
</script>

<style scoped>

</style>