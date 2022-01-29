<template>
  <div><button @click="onClick">Clicked {{counter}} times</button></div>
</template>

<script>


export default {
name:"MyButton",
data() {
    return{
        counter: 0
    }
},
methods: {
    onClick() {
        this.counter++
    },
    onmouseover(){
        console.log('Hovered on button');
    }
},
beforeCreate(){
console.log('beforeCreate');
},
created(){
console.log('created');
}, 
beforeMount() {
console.log('Component root element: ', this.$el);
},
mounted() {
    const btn = this.$el.querySelector('button');
    if(!btn) return;
    btn.addEventlistener('mouseover', this.onmouseover );
    console.log('Component root element: ', this.$el);
},
beforeUpdate(){
    console.log("beforeUpdate");
},
update(){
    console.log("update");
},
beforeDestroy(){
 const btn = this.$el.querySelector('button');
    if(!btn) return;
    btn.removeEventlistener('mouseover', this.onmouseover );
    
},
destroy(){

},
}
</script>

<style>

</style>