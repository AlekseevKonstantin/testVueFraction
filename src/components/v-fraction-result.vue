<template>
  <div class="fraction-result">
    <p class="fraction-result-numerator">{{fraction.numerator}}</p> 
    <hr class="fraction-result-bar">
    <p class="fraction-result-denominator">{{fraction.denominator}}</p>
  </div>
</template>

<script>
  export default {
    props:{
      fraction: Object
    } 
  }
</script>

<style scoped>
  .fraction-result{
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 70px;
    margin-left: 50px; 
  }

  .fraction-result-numerator,
  .fraction-result-denominator{
    width: 100%;
    padding: 9px 10px;
    border: none;
    outline: none;
    background-color: #f6eff4;
    box-sizing: border-box;
    text-align: center;
    margin: 0;
    font-size: 14px;
  }

  .fraction-result-bar{
    width: 100%;
    height: 2px;
    background-color: black;
    border: none;
  }
</style>


