<template>
    <div class="inc-exp-container">
        <div>
            <h4>Доходы</h4>
            <p id="money-plus" class="money plus">{{totalIncome}}</p>
        </div>
        <div>
            <h4>Расходы</h4>
            <p id="money-minus" class="money minus">{{totalExpense}}</p>
        </div>
    </div>
</template>

<script setup>
    const props = defineProps({
        totalIncome: {
            type: Number,
            required: true,
        },
        totalExpense: {
            type: Number,
            required: true,
        }
    });
</script>