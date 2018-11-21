<template>
   <div class="fraction-result" >{{fraction.numres}}</div>
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

    margin-left: 50px;
    padding: 10px;
    background-color: #f6eff4;
    align-self: center;
  }
</style>


