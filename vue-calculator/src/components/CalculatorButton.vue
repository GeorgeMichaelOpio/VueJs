<template>
  <button 
    :class="['calculator-button', type]"
    @click="$emit('btn-click')"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'CalculatorButton',
  props: {
    type: {
      type: String,
      default: 'number',
      validator: value => ['number', 'operator', 'function', 'equals'].includes(value)
    }
  },
  emits: ['btn-click'] // Add this line
}
</script>

<style scoped>
.calculator-button {
  border: none;
  border-radius: 12px;
  flex: 1;
  padding: 18px 5px;
  font-size: 1.5rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 60px;
}

.calculator-button:active {
  transform: translateY(2px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.number {
  background: #34495e;
  color: white;
}

.number:hover {
  background: #3d536a;
}

.operator {
  background: #3498db;
  color: white;
}

.operator:hover {
  background: #3ca0e0;
}

.function {
  background: #e74c3c;
  color: white;
}

.function:hover {
  background: #ec5c4c;
}

.equals {
  background: #2ecc71;
  color: white;
}

.equals:hover {
  background: #35d77c;
}

@media (max-width: 400px) {
  .calculator-button {
    padding: 15px 5px;
    font-size: 1.3rem;
  }
}
</style>