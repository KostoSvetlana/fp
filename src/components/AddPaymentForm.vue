<template>
  <div class="wrapper">
  <div  v-if="isElVisible">
   <input placeholder="Value" v-model.number="value" />
    <div class="select">
      <select v-model="category">
        <option v-for="(option, idx) in options" :key="idx">{{ option }}</option>
      </select>
    </div>
    <input placeholder="Date" v-model="date" />
    <button @click="onSaveClick">Save</button>
    </div>
   <hr/>
   <button @click="toggleElement">ADD NEW COST+</button>
   <hr/>
  </div>
 
</template>

<script >

export default {
name: "AddPaymentForm",
data(){
    return{
      isElVisible: false,
        value:0,
        category:"",
        date:""
       
    };
},
computed:{
getCurrentDate(){
    const today = new Date();
      const d = today.getDate();
      const m = today.getMonth() + 1;
      const y = today.getFullYear();
      return `${d}.${m}.${y}`;

},
options(){
      return this.$store.getters.getCategoryList
    }
},
 methods: {
   toggleElement(){
this.isElVisible = !this.isElVisible
   },
    onSaveClick () {
      const data = {
        id: Date.now(),
          value: this.value,
          category: this.category,
          date: this.date || this.getCurrentDate,

      };
      this.$emit('addPayment', data)
      this.$store.commit('addDataToPaymentsList', data)
  },
 },
  async created() {
    if(!this.options.length) {
      await this.$store.dispatch('loadCategories')
    }
    this.category = this.options[0]
  },
};
</script>

<style land="scss" scoped>

</style>