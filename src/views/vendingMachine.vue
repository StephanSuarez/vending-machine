<template>
  <div class="vending-machine">
    <div class="board">
      <p id="board-text">{{ validMsg }}</p>
    </div>
    <div class="showcase-container">
      <showCase :inputAut="inputAut"/>
    </div>
    <div class="input-aut">
      <input type="text" placeholder="Ingrese el código del producto" v-model="inputAut" @input="handleInput">
      <button @click="purchaseProduct">Reiniciar</button>
    </div>
    <div class="saldo">
      <p>SALDO: <span>{{ saldo }}</span></p>
    </div>
  </div>

</template>

<script>
import showCase from './showCase.vue';

export default {
  name: 'vendingMachine',
  data(){
    return {
      inputAut: '',
      validMsg: 'La palabra no es automata',
      saldo: 0
    }
  },
  components: {
    showCase,
  },
  methods: {
    purchaseProduct() {
      this.inputAut= ''
      this.saldo=0
    },
    handleInput() {
      console.log(this.inputAut);
      if(this.isValidCodeOne()){
        if (this.isValidCodeTwo()) {
          this.transitionState();
          this.validateShops()
        } else {
          this.validMsg = 'La palabra no es automata'
        }
      }
    },
    isValidCodeTwo() {
      const alphabet = /^(pm|pu|cl|cc)[01]*$/ ;
      const match = this.inputAut.match(alphabet);

      return match !== null;
    },
    isValidCodeOne(){
      if(this.inputAut.substring(0, 1) == 'p' || this.inputAut.substring(0, 1) == 'c'){
        return true
      } 
      return false
    },
    transitionState() {
      const count0 = (this.inputAut.match(/0/g) || []).length;
      const count1 = (this.inputAut.match(/1/g) || []).length;

      this.saldo = count0 * 500 + count1 * 1000;  
    },
    validateShops() {
      if (this.inputAut.substring(0, 2) == 'pm' ) {
        if (this.saldo === 2000 || this.saldo === 4000 || this.saldo === 5000) {
          this.validMsg = 'La palabra es automata';
        }else{
          this.validMsg = 'La palabra no es automata'
        }
      }
      if (this.inputAut.substring(0, 2) == 'pu' ) {
        if (this.saldo === 2000 || this.saldo === 2500 || this.saldo === 5000) {
          this.validMsg = 'La palabra es automata';
        }else{
          this.validMsg = 'La palabra no es automata'
        }
      }
      if (this.inputAut.substring(0, 2) == 'cc' ) {
        if (this.saldo === 3500 || this.saldo === 5000) {
          this.validMsg = 'La palabra es automata';
        }else{
          this.validMsg = 'La palabra no es automata'
        }
      }
      if (this.inputAut.substring(0, 2) == 'cl' ) {
        if (this.saldo === 3000) {
          this.validMsg = 'La palabra es automata';
        }else{
          this.validMsg = 'La palabra no es automata'
        }
      }
    },
  },


};
</script>

<style scoped>
.vending-machine, .saldo{
  display: flex;
  flex-direction: column;
  align-items: center;
}

.vending-machine{
  background-color: #fff;
  width: 500px;
  margin: auto;
  border-radius: 20px;
  padding-bottom: 15px;
}

.board {
  margin: 20px 0;
}

.showcase-container {
  margin: 20px 0;
}

.input-aut {
  margin-top: 20px;
  display: flex;
  align-items: center;
}

input {
  padding: 10px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
