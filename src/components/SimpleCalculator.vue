<template>
  <div class="calculator card mx-auto mt-5 p-3" style="width: 320px">
    <div class="display bg-dark text-white text-right p-3 mb-3">
      {{ current }}
    </div>
    <div class="buttons">
      <div class="row mb-2">
        <button class="btn btn-secondary col" @click="clear">C</button>
        <button class="btn btn-secondary col" @click="appendOperator('/')">
          /
        </button>
        <button class="btn btn-secondary col" @click="appendOperator('*')">
          *
        </button>
        <button class="btn btn-danger col" @click="deleteLast">DEL</button>
      </div>
      <div class="row mb-2" v-for="row in numberGrid" :key="row">
        <button
          v-for="num in row"
          :key="num"
          class="btn btn-light col"
          @click="appendNumber(num)"
        >
          {{ num }}
        </button>
      </div>
      <div class="row">
        <button class="btn btn-secondary col" @click="appendOperator('-')">
          -
        </button>
        <button class="btn btn-secondary col" @click="appendOperator('+')">
          +
        </button>
        <button class="btn btn-primary col" @click="calculate">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "0",
      previous: "",
      operator: null,
      operatorClicked: false,
      numberGrid: [
        ["7", "8", "9"],
        ["4", "5", "6"],
        ["1", "2", "3"],
        ["0", ".", ""],
      ],
    };
  },
  methods: {
    clear() {
      this.current = "0";
    },
    deleteLast() {
      this.current = this.current.slice(0, -1) || "0";
    },
    appendNumber(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current =
        this.current === "0" && number !== "." ? number : this.current + number;
    },
    appendOperator(op) {
      if (this.current === "0" && op === "-") {
        this.current = "-";
      } else {
        this.previous = this.current;
        this.operator = op;
        this.operatorClicked = true;
      }
    },
    calculate() {
      let result;
      const prev = parseFloat(this.previous);
      const curr = parseFloat(this.current);

      if (isNaN(prev) || isNaN(curr)) return;

      switch (this.operator) {
        case "+":
          result = prev + curr;
          break;
        case "-":
          result = prev - curr;
          break;
        case "*":
          result = prev * curr;
          break;
        case "/":
          result = prev / curr;
          break;
        default:
          return;
      }
      this.current = String(result);
      this.previous = "";
      this.operator = null;
    },
  },
};
</script>

<style scoped>
.calculator .btn {
  font-size: 1.2rem;
  padding: 1rem;
  margin: 0.2rem;
}
.display {
  font-size: 1.5rem;
  font-family: monospace;
}
.row {
  margin-left: auto !important;
  margin-right: auto !important;
}
</style>
