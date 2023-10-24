<template>
  <div class="bg-blue-200 p-4">
    <h1 class="text-xl font-bold">Parent Component</h1>
    <p>{{ message }}</p>
    <ChildComponent :message="message" @messageEmitted="handleMessageEmitted" />
  </div>
</template>

<script>
import { ref, defineProps, defineEmits, watch } from 'vue';
import ChildComponent from './components/ChildComponent.vue';

export default {
  components: {
    ChildComponent,
  },
  setup(props, context) {
    const message = ref(props.message);
    
    const handleMessageEmitted = (emittedMessage) => {
      message.value = emittedMessage;
    };

    watch(
      () => message.value,
      (newVal) => {
        context.emit('update:message', newVal);
      }
    );

    return {
      message,
      handleMessageEmitted,
    };
  },
};
</script>
