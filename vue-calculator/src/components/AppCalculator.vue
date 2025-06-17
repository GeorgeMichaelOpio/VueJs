<template>
  <div class="calculator">
    <Display :current="currentDisplay" :history="historyDisplay" />
    <Keypad 
      @append="append"
      @operation="setOperation"
      @calculate="calculate"
      @clear="clear"
      @backspace="backspace"
      @toggle-sign="toggleSign"
      @percent="percent"
    />
  </div>
</template>

<script>
import Display from './CalculatorDisplay.vue'
import Keypad from './CalculatorKeypad.vue'

export default {
  name: 'AppCalculator',
  components: {
    Display,
    Keypad
  },
  data() {
    return {
      currentInput: '',
      previousInput: '',
      operation: null,
      shouldReset: false
    }
  },
  computed: {
    currentDisplay() {
      if (this.currentInput === '' && this.previousInput === '') return '0'
      return this.currentInput || this.previousInput
    },
    historyDisplay() {
      if (!this.previousInput || !this.operation) return ''
      return `${this.previousInput} ${this.getOperationSymbol(this.operation)}`
    }
  },
  methods: {
    getOperationSymbol(op) {
      const symbols = {
        '+': '+',
        '-': '−',
        '*': '×',
        '/': '÷'
      }
      return symbols[op] || op
    },
    append(value) {
      if (this.shouldReset) {
        this.currentInput = ''
        this.shouldReset = false
      }
      
      if (value === '.' && this.currentInput.includes('.')) return
      if (this.currentInput === '0' && value !== '.') this.currentInput = ''
      
      this.currentInput += value
    },
    setOperation(op) {
      if (this.currentInput === '') return
      
      if (this.previousInput !== '' && !this.shouldReset) {
        this.calculate()
      }
      
      this.operation = op
      this.previousInput = this.currentInput
      this.currentInput = ''
    },
    calculate() {
      if (this.operation === null || this.shouldReset) return
      
      const prev = parseFloat(this.previousInput)
      const current = parseFloat(this.currentInput)
      
      if (isNaN(current)) return
      
      let result
      switch (this.operation) {
        case '+': result = prev + current; break
        case '-': result = prev - current; break
        case '*': result = prev * current; break
        case '/': result = prev / current; break
        default: return
      }
      
      // Round to handle floating point precision issues
      result = Math.round(result * 10000000000) / 10000000000
      
      this.currentInput = result.toString()
      this.previousInput = ''
      this.operation = null
      this.shouldReset = true
    },
    clear() {
      this.currentInput = ''
      this.previousInput = ''
      this.operation = null
      this.shouldReset = false
    },
    backspace() {
      this.currentInput = this.currentInput.slice(0, -1)
    },
    toggleSign() {
      if (this.currentInput === '') return
      if (this.currentInput.startsWith('-')) {
        this.currentInput = this.currentInput.slice(1)
      } else {
        this.currentInput = '-' + this.currentInput
      }
    },
    percent() {
      if (this.currentInput === '') return
      const value = parseFloat(this.currentInput) / 100
      this.currentInput = value.toString()
    }
  }
}
</script>

<style scoped>
.calculator {
  background: #2c3e50;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
  padding: 25px;
  width: 100%;
  max-width: 350px;
  margin: 0 auto;
}
</style>