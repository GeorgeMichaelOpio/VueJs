<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="-expenses" />
    <TranscationList :transactions="transactions" @transactionDeleted="handletransactionDeleted" />
    <AddTransaction @transactionSubmitted="handletransactionSubmitted" />
  </div>
</template>

<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TranscationList from './components/TranscationList.vue';
  import AddTransaction from './components/AddTransaction.vue';
  import { ref,computed,onMounted } from 'vue';
  import { useToast } from "vue-toastification";

  const toast = useToast();

  const transactions =  ref([]);

  onMounted(()=>{
    const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
    if (savedTransactions) {
      transactions.value = savedTransactions;
    }
  });

  	//Get Total Amount
  const total = computed(() => {
    return transactions.value.reduce((acc,transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
  });
  //Get Income and Expenses
  const income = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

const expenses = computed(() => {
  return transactions.value
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Add Transaction
  const handletransactionSubmitted = (transactionData) => {
    const newTransaction = {
      id: generateUniqueId(),
      text: transactionData.text,
      amount: Number(transactionData.amount)
    };
    transactions.value.push(newTransaction);
    saveTrasactionsToLocalStorage();
    toast.success('Transaction Added');
  

    //Generate Unique Id
    function generateUniqueId() {
      return Math.floor(Math.random() * 10000000000);
    }
  };

  //Delete Transaction
  const handletransactionDeleted = (id) => {
    transactions.value = transactions.value.filter(transaction => transaction.id !== id);
    saveTrasactionsToLocalStorage();
    toast.error('Transaction Deleted');
  };

  //save to local storage
  const saveTrasactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));};
</script>