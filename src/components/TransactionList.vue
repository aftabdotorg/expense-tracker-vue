<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="{ text, id, amount } in transactions" v-bind:key="id" :class="amount < 0 ? 'minus' : 'plus'">
            {{ text }} <span>${{ amount }}</span>
            <button class="delete-btn" @click="deleteTransaction(id)">x</button>
        </li>
    </ul>
</template>

<script setup>
const emit = defineEmits(['transactionDeleted']);
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
});

const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
}

</script>