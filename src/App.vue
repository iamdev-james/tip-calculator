<template>
  <main id='main'>
    <h1 style= 'text-align: center;' class= 'welcome MB-20 MT-40'>WELCOME</h1>
    <div class='OP-7'>
      <span class = 'MT-40 F-22 welcome'>SPLI</span>
      <p class = 'MT-10 MB-20 F-22 welcome'>TTER</p>
    </div>
    <div>
      <div id='container'>
        <div id='input'>
         <div class='MB-20'>
          <div class= 'flex_row_util'>
          <p class='OP-7 ML-13'> Bill </p>
          <p v-show= 'inputErrorAmount' style = 'color: red; margin-right: 14px;'>Can't be zero</p>
          </div>
          <input v-model= 'totalAmount' type='number' placeholder='0  ' :class = '{ borderdanger : inputErrorAmount }' class='input amount_input'>
         </div>
         <div class='OP-83'>
          <p class='selectTip'>Select Tip %</p>
          <div id='tip_block'>
            <p class='percent_btn' @click = 'setTipPercent("5")'> 5% </p>
            <p class='percent_btn' @click = 'setTipPercent("10")'> 10% </p>
            <p class='percent_btn' @click = 'setTipPercent("15")'> 15% </p>
            <p class='percent_btn' @click = 'setTipPercent("25")'> 25% </p>
            <p class='percent_btn' @click = 'setTipPercent("50")'> 50% </p>
            <div class='custom_container'>
            <p class='percent_btn custom_btn' @click = 'showCustomInput()'> Custom </p>
            <input v-model.trim = 'valueInputCustom' v-show= 'show_custom_input' class='custom_input' type= number @keydown.delete = 'monocha()' >
          </div>
          </div>
            <p v-show ='custom_input_error' style= 'color: red;'> Percent too high </p>
          </div>
          <div class='MT-20'>
          <div class= 'flex_row_util'>
          <p class='OP-7 ML-13'> Number of people </p>
          <p v-show= 'inputErrorTip' style = 'color: red; margin-right: 14px;'>Can't be zero</p>
          </div>
          <input v-model='totalPerson' type='number' placeholder='0   '  :class = '{ borderdanger : inputErrorTip }' class='input person_input'> 
        </div>
        </div>
        <div id='result'>
          <div id= 'result_container' class='result_container'>
            <div id='tip_container' class= 'flex_row'>
             <div class= 'F-17'>
              <p>Tip Amount</p>
              <p class= 'OP-7'>/ person</p>
            </div>
            <div>
              <h1>$ {{ tipPPerson }} </h1>
            </div>
            </div>
            <div id='total_container' class='flex_row'>
             <div class= 'F-17'>
              <p>Total Amount</p>
              <p class = 'OP-7'>/ person</p>
            </div>
            <div>
              <h1>$ {{ totalPPerson }} </h1>
            </div>
            </div>
          <div id='btn_container'>
            <button class='btn' @click = 'resetBtn()'> RESET </button>
          </div>
        </div>
      </div>
      </div>
    </div>
    <footer class= 'welcome'>Designed by <b> Dev. James </b></footer>
  </main>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      totalAmount: '',
      totalPerson: '',
      tipPPerson: 0.00,
      totalPPerson: 0.00,
      show_custom_input: false,
      valueInputCustom: '',
      disableInput: false,
      tipPercent: 1,
      inputErrorTip: false,
      inputErrorAmount: false,
      custom_input_error: false
    }
  },
  methods: {
    showCustomInput () {
      this.show_custom_input = true;
    },
    setTipPercent ( valueInput ) {
      this.show_custom_input = false
      this.tipPercent = valueInput
     if (!this.totalPerson || this.totalPerson <= 0) {
       this.inputErrorTip = true
     } else if ( this.totalAmount <= 0 || !this.totalAmount ) {
       this.inputErrorAmount
     } else {
       this.inputErrorTip = false
       this.inputErrorAmount = false
       this.calculateTipPPerson()
       this.calculateTotalPPerson()
     }
    },
    monocha () {
      this.disableInput = false
    },
    calculateTipPPerson () {
      let tip = this.tipPercent / 100
      let tipPerson = (tip * this.totalAmount) / this.totalPerson
      this.tipPPerson = parseFloat(tipPerson).toFixed(2)
    },
    calculateTotalPPerson () {
      let total = this.tipPPerson + this.totalAmount
      let totalPerPerson = total / this.totalPerson 
      this.totalPPerson = parseFloat(totalPerPerson).toFixed(2)
    },
    resetBtn () {
      window.location.reload()
    }
  },
  watch: {
    valueInputCustom () {
      this.custom_input_error = false
      this.inputErrorTip = false
      this.inputErrorAmount = false
      this.tipPercent = this.valueInputCustom 
      if (!this.totalPerson || this.totalPerson <= 0) {
       this.inputErrorTip = true
     } else if (this.totalAmount <= 0 || !this.totalAmount) {
       this.inputErrorAmount = true;
     } else if ( this.valueInputCustom > 200) {
       this.custom_input_error = true
     } else {
       this.inputError = false
       this.calculateTipPPerson()
       this.calculateTotalPPerson()
     }
    },
    totalAmount () {
      this.custom_input_error = false
      this.inputErrorTip = false
      this.inputErrorAmount = false
      if (!this.totalPerson || this.totalPerson <= 0) {
       this.inputErrorTip = true
     } else if (this.totalAmount <= 0 || !this.totalAmount) {
       this.inputErrorAmount = true;
     } else if ( this.valueInputCustom > 200) {
       this.custom_input_error = true
     } else {
       this.inputError = false
       this.calculateTipPPerson()
       this.calculateTotalPPerson()
     }
    },
    totalPerson () {
      this.custom_input_error = false
      this.inputErrorTip = false
      this.inputErrorAmount = false
      if (!this.totalPerson || this.totalPerson <= 0) {
       this.inputErrorTip = true
     } else if (this.totalAmount <= 0 || !this.totalAmount) {
       this.inputErrorAmount = true;
     } else if ( this.valueInputCustom > 200) {
       this.custom_input_error = true
     } else {
       this.inputError = false
       this.calculateTipPPerson()
       this.calculateTotalPPerson()
     }
    }
}
}
</script>

<style scoped>
  #main {
    font-family: 'Ubuntu Mono', monospace;
    width: 100vw;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    overflow-x: hidden;
    background: linear-gradient(90deg, #403a3e, #be5869);
  }
  #container {
    background: whitesmoke;
    height: 21rem;
    width: 40rem;
    padding: 9px 9px;
    padding-left: 25px;
    border-radius: 15px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    animation: hotAnimation 3s ease-in-out 1 forwards;
  }
  #input {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
  #result {
    height: 18rem;
    width: 28rem;
    background: #5D5C61;
    border-radius: 15px;
    margin-left: 30px;
    flex: 1;
  }
  #tip_block {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 8px;
  }
  .percent_btn {
    background: #2E1114;
    font-size: 18px;
    font-weight: 600;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 40px;
    cursor: pointer;
    border-radius: 7px;
  }
  .percent_btn:hover {
    background: #2E1157
  }
  .custom_container {
    position: relative;
  }
  .custom_btn {
    width: 100px;
    position: absolute;
    background: whitesmoke;
    color: #2E1114;
    border: 1px solid #2E1114;
  }
  .custom_input {
    position: absolute;
    height: 40px;
    width: 100px;
    font-size: 18px;
    border: none;
    outline-color: skyblue;
    text-align: center;
  }
  .amount_input {
    background: url('~@/assets/dollar.png') no-repeat 8px center / cover;
    background-size: 15px;
    opacity: 0.726;
  }
  .person_input {
    background: url('~@/assets/user.png') no-repeat 8px center / cover;
    background-size: 15px;
    opacity: 0.726;
  }
  /* UTILITY CLASS*/
  .MT-40 {
    margin-top: 40px;
  }
  .MT-20 {
    margin-top: 20px;
  }
  .MT-10 {
    margin-top: 10px;
  }
  .MB-20 {
    margin-bottom: 20px;
  }
  .OP-7 {
    opacity: 0.7;
  }
  .OP-83 {
    opacity: 0.83;
  }
  .F-17 {
    font-size: 17px;
    font-weight: 500;
  }
  .F-22 {
    font-size: 22px;
    font-weight: 600;
  }
  .welcome {
    color: white;
    text-shadow: 2px 2px 4px #403a3e;
  }
  .input {
    background-color: lightblue; 
    color: green;
    width: 19rem;
    height: 2rem;
    border: none;
    font-size: 18px;
    outline-color: skyblue;
    text-align: right;
    padding-right: 15px;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
  }
  .flex_row {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    margin-top: 25px;
    color: lightgreen;
  }
  .flex_row_util {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
  .result_container {
    width: 100%;
    height: 100%;
  }
  .btn_container {
    width: 100%;
    height: 100%;
    margin: auto;
  }
  .btn {
    margin-top: 103px;
    margin-left: 4%;
    border: none;
    text-align: center;
    padding:10px 90px;
    background: #83677B;
    color: white;
    font-size: 18px;
  }
  .borderdanger {
  border: 1px dashed red;
  border-radius: 8px;
  outline: none;
  }
  footer{
    margin-top: 30px;
    text-align: center;
    color: black;
    font-size: 18px;
  }

  /* ANIMATION */
  @keyframes hotAnimation {
    0% {
      transform: rotate(30deg);
    }
    25% {
      transform: rotate(-30deg);
    }
    50% {
      transform: rotate(0deg)
    }
    75% {
      transform: scale(1.2);
    }
    100% {
      transform: scale(1);
    }
  }

  @media only screen and (max-width: 700px) {
    #main {
      height: 100vh;
      overflow-x: hidden;
      background: linear-gradient(15deg, #403a3e, #be5869);
    }
    #container {
      width: 90vw;
      height: 39rem;
      flex-direction: column;
      padding-left: 12px;
    }
    #result {
      margin: auto;
      margin-top: 20px;
      width: 70vw;
      justify-self: center;
      align-self: center;
    }
    .btn {
      margin-left: 23%;
    }
    .selectTip {
      margin-bottom : 8px;
    }
  }
  @media only screen and (max-width: 500px) {
    .btn {
      margin-left: 10%;
      margin-bottom: 11px;
    }
    .MT-40 {
      margin-top: 100px;
    }
  }
  @media only screen and (max-width: 400px) {
    .input {
      width: 17rem;
      margin-left : 7px;
    }
    .ML-13 {
      margin-left : 13px;
    }
    #tip_block {
      grid-template-columns: repeat(3, 85px);
    }
    .btn {
      margin-left: 4%;
    }
    .custom_input, .custom_btn {
      width: 85px;
    }
    .MT-40 {
      margin-top: 150px;
    }
  }
  @media only screen and (max-width: 330px) {
    .input {
      width: 15rem;
      margin-left : 5px;
    }
    .ML-13 {
      margin-left : 13px;
    }
    #tip_block {
      grid-template-columns: repeat(3, 75px);
    }
    .btn {
      margin-left: 3%;
      padding: 10px 75px;
    }
    .custom_input, .custom_btn {
      width: 75px;
    }
    .selectTip {
      margin-bottom: 10px;
    }
    .MT-40 {
      margin-top: 200px;
    }
  }
  @media only screen and (max-width: 281px) {
    .input {
      width: 13rem;
      margin-left : 5px;
    }
    .ML-13 {
      margin-left : 13px;
    }
    #tip_block {
      grid-template-columns: repeat(3, 65px);
    }
    .btn {
      margin-left: 4%;
      padding: 10px 66px;
    }
    .custom_input, .custom_btn {
      width: 65px;
    }
    .selectTip {
      margin-bottom: 8px;
    }
    .MT-40 {
      margin-top: 180px;
    }
  }
</style>
