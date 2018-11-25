<template>
  <div id="app">
    <h1>Вычисление суммы простых дробей</h1>
    <form class="fraction-form">
      <div class="fraction-expression-wrapper"> 
        <div class="fraction-expression">
          <app-fraction v-for="(fraction, index) in fractions"
                        v-bind:key="index"
                        v-bind:fraction="fraction">
          </app-fraction>
        </div>

        <component v-bind:is="component" 
                   v-bind:fraction="result"
                   v-show="calсСompleted"> 
        </component>
        
      </div>
      <div class="fraction-form-controlls">
        <button class="fraction-form-controlls__add-btn"
                v-on:click.prevent="addFraction">
                add new element
        </button>
        <button class="fraction-form-controlls__delete-btn"
                v-on:click.prevent="deleteFraction">
                delete element
        </button>
      </div>
    </form>    
  </div>
</template>

<script>

import Fraction from "./components/v-fraction.vue";
import FractionResult from "./components/v-fraction-result.vue";
import FractionSimpleResult from "./components/v-fraction-simple-result.vue";

export default {
  name: 'app',
  data () {
    return {
      fractions: 
      [{
          numerator: '',
          denominator: '',
          checked: false,
          checkShow: false
        },
        {
          numerator: '',
          denominator: '',
          checked: false,
          checkShow: false
      }],

      calсСompleted: false,
      component: 'app-fraction-simple-result'
     
    }
  },
  methods:{
    
    nod(x, y) {
      while (y !== 0) y = x % (x = y);
      return x;
    },

    nok(array) {
      let n = array.length,
          a = Math.abs(parseFloat(array[0]));

      for (let i = 1; i < n; i++) {
          let b = Math.abs(parseFloat(array[i])),
              c = a;
          while (a && b) {
              a > b ? a %= b : b %= a;
          }
          a = Math.abs(c * parseFloat(array[i]) / (a + b));
      }
      return a;
    },

    addFraction(){

      if(this.fractions.length < 5){

        let res = { numerator: '',
                  denominator: '',
                  checked: false,
                  checkShow: false
                };
        
        this.calсСompleted = false;

        if(this.fractions.length >= 2){

          for (let i = 0; i < this.fractions.length; i++) {
            this.fractions[i].checkShow = true;
          }
          res.checkShow = true;
        }
        this.fractions.push(res);
      }
    },

    deleteFraction(){

      let countChecked = 0;
      for (let i = 0; i < this.fractions.length; i++) {
        if(this.fractions[i].checked){
          countChecked += 1;    
        }
      }

      if(countChecked == this.fractions.length || countChecked == this.fractions.length-1){
        alert('Необходимо оставить хотя бы две дроби!');
        return;
      } 

      for (let i = 0; i < this.fractions.length; i++) {
        if(this.fractions[i].checked){
          this.fractions.splice(i , 1);
          i -= 1;
        }
      }

      if(this.fractions.length <= 2){
        for (let i = 0; i < this.fractions.length; i++) {
          this.fractions[i].checkShow = false;
        }
      }
    }
  },
  computed:{

    result(){
      
      let denominators = [],
          numerators = [];
      
      let res = { numerator: '',
                  denominator: '',
                  numres: ''
                };

      for (let i = 0; i < this.fractions.length; i++) {
        if(this.fractions[i].numerator === '' || this.fractions[i].denominator === ''){
          this.calсСompleted = false;
          return res;
        }

        denominators.push(parseFloat(this.fractions[i].denominator));
        numerators.push(parseFloat(this.fractions[i].numerator));
      }

      let resNOK = this.nok(denominators);

      for (let i = 0; i < numerators.length; i++) {
        numerators[i] = numerators[i] * (resNOK / denominators[i]);
      }

      let result = 0;
      for (let i = 0; i < numerators.length; i++) {
        result += numerators[i];
      }

      this.calсСompleted = true;
      
      if(result % resNOK == 0){

        this.component = 'app-fraction-simple-result';
        res.numres = result / resNOK;
        return res;
      } 

      let resNOD = this.nod(result, resNOK);

      if(resNOD !== 1){

        result = result / resNOD;
        resNOK = resNOK / resNOD;
      }

      this.component = 'app-fraction-result';
      res.numerator = result;
      res.denominator = resNOK;
      return res;
    }
  },
  components:{

    'app-fraction': Fraction,
    'app-fraction-result': FractionResult,
    'app-fraction-simple-result': FractionSimpleResult 
  }
}
</script>

<style>

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  h1, h2 {
    font-weight: normal;
  
  }

  h1{
    margin-bottom: 75px;
  }

  .fraction-form{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .fraction-expression,
  .fraction-expression-wrapper{
    display: flex;
    justify-content: center;
    align-items: flex-start;
  }

  .fraction-expression-result{
    margin-left: 50px;
  }

  .fraction-form-controlls{
    margin-top: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .fraction-form-controlls__add-btn,
  .fraction-form-controlls__delete-btn{
    border: none;
    outline: none;
    box-shadow: none;
    padding: 10px 20px;
    border-radius: 2px;
  }

  .fraction-form-controlls__add-btn:hover,
  .fraction-form-controlls__delete-btn:hover{
    cursor: pointer;
  }

  .fraction-form-controlls__delete-btn{
    margin-left: 40px;
  }

</style>
