<template>
    <h4>Баланс</h4>
    <h1 id="balance">{{ totalBalance }}</h1>
</template>

<script setup>
    const props = defineProps({
        totalBalance: {
            type: Number,
            required: true,
        }
    });
</script>