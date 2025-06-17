<template>
  <div class="keypad">
    <div class="row">
      <Button type="function" @btn-click="$emit('clear')">C</Button>
      <Button type="function" @btn-click="$emit('backspace')">⌫</Button>
      <Button type="function" @btn-click="$emit('percent')">%</Button>
      <Button type="operator" @btn-click="$emit('operation', '/')">÷</Button>
    </div>
    
    <div class="row">
      <Button type="number" @btn-click="$emit('append', '7')">7</Button>
      <Button type="number" @btn-click="$emit('append', '8')">8</Button>
      <Button type="number" @btn-click="$emit('append', '9')">9</Button>
      <Button type="operator" @btn-click="$emit('operation', '*')">×</Button>
    </div>
    
    <div class="row">
      <Button type="number" @btn-click="$emit('append', '4')">4</Button>
      <Button type="number" @btn-click="$emit('append', '5')">5</Button>
      <Button type="number" @btn-click="$emit('append', '6')">6</Button>
      <Button type="operator" @btn-click="$emit('operation', '-')">−</Button>
    </div>
    
    <div class="row">
      <Button type="number" @btn-click="$emit('append', '1')">1</Button>
      <Button type="number" @btn-click="$emit('append', '2')">2</Button>
      <Button type="number" @btn-click="$emit('append', '3')">3</Button>
      <Button type="operator" @btn-click="$emit('operation', '+')">+</Button>
    </div>
    
    <div class="row">
      <Button type="number" @btn-click="$emit('toggle-sign')">±</Button>
      <Button type="number" @btn-click="$emit('append', '0')">0</Button>
      <Button type="number" @btn-click="$emit('append', '.')">.</Button>
      <Button type="equals" @btn-click="$emit('calculate')">=</Button>
    </div>
  </div>
</template>

<script>
import CalculatorButton from './CalculatorButton.vue'

export default {
  name: 'CalculatorKeypad',
  components: {
    Button: CalculatorButton
  },
  emits: [
    'append', 
    'operation', 
    'calculate', 
    'clear', 
    'backspace', 
    'toggleSign',
    'percent'
  ]
}
</script>

<style scoped>
.keypad {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.row {
  display: flex;
  justify-content: space-between;
  gap: 12px;
}
</style>