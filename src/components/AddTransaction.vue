<template>
    <h3>Добавить транзакцию</h3>
        <form id="form" @submit.prevent="onSubmit">
            <div class="form-control">
                <label for="text">Наименование</label>
                <input type="text" id="text" v-model="text" placeholder="Введите наименование..." />
            </div>
            <div class="form-control">
                <label for="amount">
                    Сумма <br />
                    (- расход, + доход)
                </label>
                <input type="text" id="amount" v-model="amount" placeholder="Введите сумму..." />
            </div>
            <button class="btn">Добавить</button>
        </form>
</template>

<script setup>
    import { ref } from 'vue';

    const text = ref('');
    const amount = ref('');

    const emit = defineEmits(['transactionSubmitted']);

    const onSubmit = () => {
        if (!text.value || !amount.value) {
            alert('Оба поля должны быть заполнены');
            return;
        }

        const transactionData = {
            text: text.value,
            amount: parseFloat(amount.value),
        };

        emit('transactionSubmitted', transactionData);

        text.value = '';
        amount.value = '';
    };
</script>