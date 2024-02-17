<template>
  <PageTitle msg="Expense Tracker" />
  <PageBalance :balance="+bal" />
  <IncomeExpense :income="+income" :expense="+expense" />
  <TransactionList :transactions="transactions" @transactionDeleted="handleTrDelete" />
  <TransactionForm  @transactionSubmitted="handleTrSubmit" />
</template>

<script setup>
/* eslint-disable */
import PageTitle from './components/PageTitle.vue';
import PageBalance from './components/PageBalance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import TransactionForm from './components/TransactionForm.vue';
import {useToast} from 'vue-toastification';
import {ref,computed,onMounted} from 'vue';

const toast = useToast();

const income = computed(() => {
  return transactions.value
    .filter((transaction)=> transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
});

const expense = computed(() => {
  return transactions.value
    .filter((transaction)=> transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
});

const bal = computed(() => {
  // Convert the string values back to numbers using parseFloat
  const incomeNumber = parseFloat(income.value);
  const expenseNumber = parseFloat(expense.value);
  
  // Now perform the addition and convert the result to a fixed decimal string
  return (incomeNumber + expenseNumber).toFixed(2);
});



const transactions = ref([]);

// save to local storage
onMounted(()=>{
  const savedTranscations = JSON.parse(localStorage.getItem('transactions'));

  if (savedTranscations){
    transactions.value = savedTranscations;
  }
});

const saveTransactionsToLocalStorage= () => {
  localStorage.setItem('transactions',JSON.stringify(transactions.value));
};

// Addtransaction function
const handleTrSubmit = (transactionData) =>{
  // console.log(transactionData);
  transactions.value.push({
    id : generateId(),
    text : transactionData.text,
    amount : transactionData.amount
  });

  saveTransactionsToLocalStorage();

  toast.success("Transaction successfully added!");
};

// deletetransaction function
const handleTrDelete = (id) =>{
  // console.log(id);
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.success("Transaction successfully deleted!");
};

const generateId = () =>{
  return Math.floor(Math.random()*100);
};
</script>

