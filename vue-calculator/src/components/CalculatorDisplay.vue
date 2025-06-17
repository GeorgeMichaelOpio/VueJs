<template>
  <div class="display">
    <div class="history">{{ history }}</div>
    <div class="current">{{ current }}</div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorDisplay',
  props: {
    current: {
      type: String,
      default: '0'
    },
    history: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
.display {
  background: #34495e;
  border-radius: 10px;
  margin-bottom: 25px;
  padding: 20px;
  text-align: right;
  box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.3);
  min-height: 100px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.history {
  color: #95a5a6;
  font-size: 1.2rem;
  min-height: 25px;
  overflow: hidden;
  text-overflow: ellipsis;
}

.current {
  color: #ecf0f1;
  font-size: 2.5rem;
  font-weight: 300;
  overflow: hidden;
  text-overflow: ellipsis;
}

@media (max-width: 400px) {
  .current {
    font-size: 2rem;
  }
}
</style>