<template>
    <h3>Транзакции</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" v-bind:key="transaction.id"
        v-bind:class="transaction.amount > 0 ? 'plus': 'minus'">
            {{transaction.text}} <span>{{transaction.amount}}</span>
            <button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
        </li>
        <!-- <li class="minus">
            Cash <span>-$400</span>
            <button class="delete-btn">x</button>
        </li>
        <li class="plus">
            Payment <span>$400</span>
            <button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<script setup>
    const emit = defineEmits(['transactionDeleted']);

    const props = defineProps({
        transactions: {
            type: Array,
            required: true,
        }
    });

    const deleteTransaction = (id) => {
        emit('transactionDeleted', id);
    }
</script>