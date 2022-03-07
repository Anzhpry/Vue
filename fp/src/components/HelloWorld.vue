<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <hr />
    <!--  <button v-on:click="doThat('hello', $event)">Click me</button>
    <button @click="doThat('hello', $event)">Click me 2</button>
    <input type="text" @blur="onValidate" /> -->
    <div class="display">
      <input v-model.number="operand1" type="number" />
      <input v-model.number="operand2" type="number" />

      = {{ result }}
    </div>
    <div class="errors" v-if="error">Ошибка: {{ error }}</div>

    <div class="keyboard">
      <button
        v-for="operand in operands"
        :key="operand"
        @click="calculate(operand)"
      >
        {{ operand }}
      </button>
      <!--     <button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('*')">*</button> -->
    </div>
    <!--  <div class="arr">
      <div v-for="(item, index) in myCollection" :key="index">
        {{ index }} - {{ item }}
      </div>
    </div>
 -->
    <!--  <input :value="operand1" @input="operand1 = $event.target.value" /> -->

    <div>
      <input type="checkbox" v-model="checkedNames" />
      <label for="keybord">Отобразить экранную клавиатуру</label>
    </div>
    <div class="checkbox-keybord">
      <button v-for="checkedName in checkedNames" :key="checkedName">
        {{ checkedName }}
      </button>
    </div>
    <div>
      <input type="radio" id="one" value="Один" v-model="picked" />
      <label for="one">Операнд 1</label>
      <input type="radio" id="two" value="Два" v-model="picked" />
      <label for="two">Операнд 2</label>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: {
      type: String,
      default: "",
      required: true,
    },
  },
  data() {
    return {
      message: "Hello Vue",
      /*   myCollection: [1, 2, 3, 4, 5, 6], */
      operands: ["+", "-", "/", "*"],
      operand1: 0,
      operand2: 0,
      error: "",
      result: 0,
      checkedNames: [1, 2, 3, 4, 5, 6],
    };
  },
  methods: {
    calculate(operation = "+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.substract();
          break;
        case "/":
          this.divide();
          break;
        case "*":
          this.multiply();
          break;
      }
    },
    add() {
      this.result = this.operand1 + this.operand2;
    },
    substract() {
      this.result = this.operand1 - this.operand2;
    },
    divide() {
      if (this.operand2 === 0) {
        this.error = "На 0 делить нельзя!";
        return;
      } else {
        this.result = this.operand1 / this.operand2;
      }
    },
    multiply() {
      this.result = this.operand1 * this.operand2;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
