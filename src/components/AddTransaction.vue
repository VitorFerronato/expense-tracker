<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="text" type="text" id="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        v-model="amount"
        type="text"
        id="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";

import { useToast } from "vue-toastification";
const toast = useToast();

const emit = defineEmits(["transactionSubmit"]);

// DATA
const text = ref("");
const amount = ref("");

// FUNCTIONS
const onSubmit = () => {
  if (!text.value || !amount.value)
    return toast.error("Both field are required");

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmit", transactionData);

  text.value = "";
  amount.value = " ";
};
</script>