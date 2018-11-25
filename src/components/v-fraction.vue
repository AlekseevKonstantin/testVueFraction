<template>
  <div class="fraction">
    <input class="fraction-numerator" 
           type="text"
           v-on:keyup="keyEnter" 
           pattern="^[0-9]+$"
           v-model.number="fraction.numerator">
    <hr class="fraction-bar">
    <input class="fraction-denominator" 
           type="text"
           v-on:keyup="keyEnter"
           pattern="^[0-9]+$"
           v-model.number="fraction.denominator">
    <input class="fraction-check" 
           type="checkbox" 
           v-model="fraction.checked"
           v-show="fraction.checkShow">       
  </div>
</template>

<script>
  
  export default {
    props:{
      fraction: Object
    },
    
    methods:{

      keyEnter(e){
        this.inputValidation(e.target);
      },

      inputValidation(elem){
   
        elem.value = elem.value.replace(/[^\d]/g, '');

        if(elem.value.length > 2){
          elem.value = elem.value.slice(0, -1);
        }
        
        if(elem.value.length > 1){
          elem.value = elem.value.replace(/^0+/, '');
        }
      }
    } 
  }
</script>

<style scoped>

  .fraction{
    position: relative;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 70px;
    margin-left: 50px;  
  }

  .fraction:not(:first-child)::before{
    content: '';
    background: url('../img/add.png') no-repeat;
    position: absolute;
    top: 27px;
    left: -58%;
    width: 32px;
    height: 32px;
  }

  .fraction:last-child::after{
    content: '';
    background: url('../img/equal.png') no-repeat;
    position: absolute;
    top: 27px;
    left: 114%;
    width: 32px;
    height: 32px;
  }

  .fraction:first-child{
    margin-left: 0;
  }

  .fraction-bar{
    width: 100%;
    height: 2px;
    background-color: black;
    border: none;
  }

  .fraction-numerator,
  .fraction-denominator{
    width: 100%;
    padding: 10px;
    border: none;
    outline: none;
    background-color: #f6eff4;
    box-sizing: border-box;
    text-align: center;
  }

  .fraction-check{
    width: 17px;
    height: 17px;
    margin-top: 10px;
  }

</style>


