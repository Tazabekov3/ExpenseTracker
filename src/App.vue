<template>
    <Header />
    <div class="container">
        <Balance :totalBalance="+totalBalance" />
        <IncomeExpenses :totalIncome="+totalIncome" :totalExpense="+totalExpense" />
        <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
</template>

<script setup>
    import Header from './components/Header.vue';
    import Balance from './components/Balance.vue';
    import IncomeExpenses from './components/IncomeExpenses.vue';
    import TransactionList from './components/TransactionList.vue';
    import AddTransaction from './components/AddTransaction.vue';

    import { ref, computed, onMounted } from 'vue';

    onMounted(() => {
        const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

        if (savedTransactions) {
            transactions.value = savedTransactions;
        }
    });

    const transactions = ref([
        // {id: 1, text: 'Flower', amount: -19.99},
        // {id: 2, text: 'Salary', amount: 499.99},
        // {id: 3, text: 'Camera', amount: -79.99},
    ]);

    const totalBalance = computed(() => {
        return transactions.value
            .reduce((acc, transaction) => {
                return acc + transaction.amount;
            }, 0);
    });

    const totalIncome = computed(() => {
        return transactions.value
            .filter((transaction) => transaction.amount > 0)
            .reduce((acc, transaction) => {
                return acc + transaction.amount;
            }, 0)
            .toFixed(2);
    });

    const totalExpense = computed(() => {
        return transactions.value
            .filter((transaction) => transaction.amount < 0)
            .reduce((acc, transaction) => {
                return acc + transaction.amount;
            }, 0)
            .toFixed(2);
    });

    const generateUniqueId = () => {
        return Math.floor(Math.random() * 1000000);
    };

    const handleTransactionSubmitted = (transactionData) => {
        transactions.value.push({
            id: generateUniqueId(),
            text: transactionData.text,
            amount: transactionData.amount,
        });

        saveTransactionsToLocalStorage();
        alert('Транзакция добавлена');
    };

    const handleTransactionDeleted = (id) => {
        transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
        
        saveTransactionsToLocalStorage();
        alert('Транзакция удалена');
    }

    const saveTransactionsToLocalStorage = () => {
        localStorage.setItem('transactions', JSON.stringify(transactions.value));
    }
</script>