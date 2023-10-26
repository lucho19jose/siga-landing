<script setup>
import { ref } from 'vue';

const name = ref('');
const email = ref('');
const phone = ref('');
const description = ref('');

async function submitForm() {
  try {
    console.log(`Name: ${name.value}, Email: ${email.value}, Description: ${description.value}`);
    const url = `https://formspree.io/f/xbjedoqv`;
    const requestOptions = {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json', // Set the appropriate content type for your API
      },
      body: JSON.stringify({
        name: name.value,
        email: email.value,
        phone: phone.value,
        description: description.value,
      })
    };

    const response = await fetch(url, requestOptions);
    const data = await response.json();
    console.log(data);
    
    name.value = '';
    phone.value = '';
    email.value = '';
    description.value = '';
    
  } catch (error) {
    console.error(error);
  }
}
</script>
<template>
  <form class="contact-form" @submit.prevent="submitForm">
    <div class="mb-3">
      <input
        class="form-input w-full rounded"
        name="name"
        type="text"
        v-model="name"
        placeholder="Nombre"
        required
      />
    </div>
    <div class="mb-3">
      <input
        class="form-input w-full rounded"
        name="email"
        type="email"
        v-model="email"
        placeholder="tu correo electronico"
        required
      />
    </div>
    <div class="mb-3">
      <input
        class="form-input w-full rounded"
        name="phone"
        type="text"
        v-model="phone"
        placeholder="Tu numero de telefono"
        required
      />
    </div>
    <div class="mb-3">
      <textarea
        class="form-textarea w-full rounded-md"
        rows="7"
        placeholder="Tu mensaje"
        v-model="description"
        ></textarea>
    </div>
    <button type="submit" class="btn btn-primary">Enviar Ahora</button>
  </form>
</template>

