<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiple" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
  export default{
    data(){
      return {
        previous: null,
        current: '',
        operator: null,
        operatorClicked: false
      }
    },

    methods: {
      set_previous() {
        this.operatorClicked = true;
        this.previous = this.current;
      },

      clear() {
        this.current = '';
      },

      sign() {
        if (this.current > 0){
          this.current = -this.current;
        }

        else if(this.current < 0){
          this.current = -this.current;
        }

        else if(this.current == 0){
          //do nothing
        }

        else{
          console.log("Something went wrong.");
        }
      },

      percent(){
        this.current = `${parseFloat(this.current) / 100}`;
      },

      append(number){  
        if(this.operatorClicked){
          this.current = '';
          this.operatorClicked = false;
        }      
          this.current = `${this.current}${number}`; 
      },

      dot(){
        if(this.current.indexOf('.') === -1){
          this.append('.');
        }
      },

      divide(){
        //this.append('/');
        this.operator = (a, b) => a / b;
        this.set_previous();
      },

      multiple(){
        //this.append('x');
        this.operator = (a, b) => a * b;
        this.set_previous();

      },

      minus(){
        //this.append('-');
        this.operator = (a, b) => a - b;
        this.set_previous();
      },

      plus(){
        //this.append('+');
        this.operator = (a, b) => a + b;
        this.set_previous();
      },

      equal() {
        this.current = `${this.operator(
          parseFloat(this.current), 
          parseFloat(this.current)
          )}`;
        this.previous = null;
      }
    }
  }
</script>

<style scoped>
.calculator{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  text-align: center;
  width: 400px;
  border: 3px solid #3b3b3b;
  -webkit-box-shadow: 1px 10px 21px 1px rgba(0,0,0,0.49); 
  box-shadow: 1px 10px 21px 1px rgba(0,0,0,0.49);
}

.display{
  grid-column: 1 / 5;
  background: rgb(63, 63, 63);
  color: #d6d6d6;
  text-align: right;
  font-size: 2.2rem;
  padding: 10px;
  background: #3b3b3b;

}

.zero{
  grid-column: 1 / 3;
}

.btn{
  background-color: #0e0e0e;
  border: solid 1px #3b3b3b;
  color: #d6d6d6;
  padding-top: 10px;
  cursor: pointer;
}

.operator{
  background-color: #0098d4;
}
</style>
