<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <!--{{massage}}
    <button @click="someMethodClick">Click</button>-->
   <input type="text" v-model.number="operand1"/>
   <input type="text" v-model.number="operand2"/>

   = {{ result }}
   <br/>
   = {{ resultFib }}
   <br/>
   <div class="message">
    <template v-if="result < 0"> Получилось отрицательное число </template>
    <template v-else-if="result < 100">Результат в первой сотне </template>
    <template v-else> Получилось слишком большое число </template>
   </div>



  <hr/>


  <button v-for="(operand, idx) in operands" @click="calculate(operand)" :key="idx"></button>
  <hr/>

{{myCollection}}
<div v-for="(operand, index) in myCollection" :key="index">
  {{index}} -- {{item}}
</div>
 {{logs}}
  


  </div>
  
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      disabled: false,
      massage:"",
      operand1:0,
      operand2:0,
      result: 0,
      resultFib: 0,
      error: '',
      myCollection: [1,2,3,5,4,6,7,9],
      operands: ['+', '-', '*', '/', '**'],
      logs: {},
      //obj:{}
    };
  },
  computed:{
    fib1(){
      return this.fib(this.operand1)
    },
    fib2(){
      return this.fib(this.operand2)
    }
  },
  methods: {
    calculate(operation="+"){
      this.error=""
switch(operation){
  case'+':
  this.add()
  break;
  case'-':
  this.substract()
  break;
  case'/':
  this.divide()
  break;
  case'*':
  this.multiply()
  break;
  case'**':
  this.pow()
  break;
    }
    //Vue.set(obj, propName, value)
    const key = Date.now()
    const value = `${this.operand1}${operation}${this.operand2} = ${this.result}`
    this.$set(this.logs, key, value)
    //this.$set(this.obj, "obj1", 'value')
    //setTimeout(()=>{
     // this.$set(this.obj, 'obj1', 'value2')
   // }, 5000)

    },
    add(){
      this.resultFib = this.fib1 + this.fib2
    this.result = this.operand1 + this.operand2;
    },
    substract(){
    this.result = this.operand1 - this.operand2;
    },
    divide(){
      const{operand1, operand2} = this
      if(operand2 === 0){
        this.error = "Делить на 0 нельзя!"
        return
      }
      this.result = operand1 / operand2;

    },
    multiply(){
    this.result = this.operand1 * this.operand2;
    },
    pow(){
    this.result = this.operand1 ** this.operand2;
    },
   fib(n){
     return n <= 1 ? n : this.fib(n-1) + this.fib (n-2)
   }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
