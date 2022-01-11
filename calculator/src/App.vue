<template>
  <div class="w-screen h-screen bg-gray-800">
    <div class="w-full h-12 fixed"></div>
    <div class="w-full h-1/3 pr-4">
      <div class="h-2/3 flex items-end justify-end text-gray-400">
        {{ calculatedValue }}
      </div>
      <div
        class="h-1/3 flex items-center justify-end text-6xl text-white font-bold"
      >
        {{ inputValue }}
      </div>
    </div>
    <div class="w-full h-2/3">
      <div
        class="grid grid-cols-4 gap-2 justify-center items-center w-full h-full p-4 pb-10 text-4xl place-content-center"
      >
        <button @click="clearAll" class="text-gray-50 bg-gray-500">AC</button>
        <button @click="clearLastNumber" class="text-gray-400 bg-gray-500">
          C
        </button>
        <button @click="separation" class="text-green-600 bg-gray-50">%</button>
        <button @click="inputData('÷')" class="text-green-600 bg-gray-50">
          &#247;
        </button>
        <button @click="inputData('7')" class="text-gray-400">7</button>
        <button @click="inputData('8')" class="text-gray-400">8</button>
        <button @click="inputData('9')" class="text-gray-400">9</button>
        <button @click="inputData('×')" class="text-green-600 bg-gray-50">
          &#215;
        </button>
        <button @click="inputData('4')" class="text-gray-400">4</button>
        <button @click="inputData('5')" class="text-gray-400">5</button>
        <button @click="inputData('6')" class="text-gray-400">6</button>
        <button @click="inputData('-')" class="text-green-600 bg-gray-50">
          -
        </button>
        <button @click="inputData('1')" class="text-gray-400">1</button>
        <button @click="inputData('2')" class="text-gray-400">2</button>
        <button @click="inputData('3')" class="text-gray-400">3</button>
        <button @click="inputData('+')" class="text-green-600 bg-gray-50">
          +
        </button>
        <button @click="unaryMinus" class="text-gray-400">&#177;</button>
        <button @click="inputData('0')" class="text-gray-400">0</button>
        <button @click="inputData('.')" class="text-gray-400">.</button>
        <button @click="inputData('=')" class="text-green-600 bg-gray-50">
          =
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      separationOn: false,
      inputValue: "0",
      calculatedValue: "",
    };
  },
  methods: {
    inputData(data) {
      switch (data) {
        case "÷":
        case "×":
        case "-":
        case "+":
          this.separationOn = true;
          this.calculatedValue = `${this.calculatedValue}${this.inputValue} ${data} `;
          this.inputValue = eval(
            this.calculatedValue.substring(0, this.calculatedValue.length - 2)
          );
          console.log(this.calculatedValue[this.calculatedValue.length - 2]);
          break;
        case "=":
          this.separationOn = true;
          this.calculatedValue = this.calculatedValue
            .replace("÷", "/")
            .replace("×", "*");
          this.inputValue = eval(`${this.calculatedValue} ${this.inputValue}`);
          this.calculatedValue = "";
          break;
        default:
          if (this.separationOn) {
            this.inputValue = "";
            this.separationOn = false;
          }
          this.inputValue === "0" && data !== "."
            ? (this.inputValue = data)
            : (this.inputValue += data);
      }
    },
    clearAll() {
      this.inputValue = "0";
      this.calculatedValue = "";
    },
    clearLastNumber() {
      if (this.inputValue.length === 1) this.inputValue = "0";
      else
        this.inputValue = this.inputValue.substring(
          0,
          this.inputValue.length - 1
        );
    },
    unaryMinus() {
      this.inputValue = String(-this.inputValue);
    },
    separation() {
      this.separationOn = true;
      this.inputValue =
        eval(
          this.calculatedValue.substring(0, this.calculatedValue.length - 2)
        ) *
        (this.inputValue / 100);
    },
  },
};
</script>

<style>
button {
  border-radius: 100%;
  transition: 100ms;
  height: 75px;
  width: 75px;
}

button:hover {
  background-color: silver;
}
</style>
