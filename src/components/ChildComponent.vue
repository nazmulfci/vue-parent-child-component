<template>
    <div class="bg-green-200 p-4 mt-4">
      <h2 class="text-lg font-bold">Child Component</h2>
      <p>{{ message }}</p>
      <button @click="emitMessage">Emit Message</button>
    </div>
  </template>
  
  <script>
  import { ref, defineProps, defineEmits } from 'vue';
  
  export default {
    props: {
      message: String,
    },
    setup(props, context) {
      const message = ref(props.message);
  
      const emitMessage = () => {
        const customMessage = 'Hello from ChildComponent!';
        message.value = customMessage;
        context.emit('messageEmitted', customMessage);
      };
  
      return {
        message,
        emitMessage,
      };
    },
  };
  </script>
  