<template>
    <!-- <div> element is binding the class "is-complete" to the prop "propLineItem" completed value (boolean: true or false) -->
    <div class="line-item" v-bind:class="{'is-complete':propLineItem.completed}">
        <p>
            <!--- Input element is a checkbox field that calls the "markComplete" method when changed using v-on  --->
            <input type="checkbox" v-on:change="markComplete">
            <!--- using interpolation {{.....}} to display dynamic data from the prop "propLineItem", the title in this case --->
            {{propLineItem.title}}
            <!--- button element that emits the "del-line-item" emitter and "propLineItem.id" when clicked ising @click.
                the emitter is caught by the parent component <LineItemList> using v-on --->
            <button @click="$emit('del-line-item', propLineItem.id)" class="del">X</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "LineItem",
    props: { //props is an object containing props in format of propname:data-type
        propLineItem: Object
    },
    methods: { //Methods object containing the methods usind in this component
        markComplete(){
            this.propLineItem.completed = !this.propLineItem.completed; //reverses the completed status of the line item's current status when called (true -> false, or false -> true)
        }
    }

}
</script>

<style scoped>
.line-item{
    background: #f4f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
}

.is-complete{
    text-decoration: line-through;
}

.del{
    background: #ff0000;
    color: #fff;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    float: right;
}
</style>