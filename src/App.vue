<template>
  <div id="app">
    <SideBarComponent />
    <router-view /> <!-- This will render the matched component (e.g., PrescriptionBill) -->
    <Chatbot /> <!-- Add Chatbot here to use it -->
  </div>
</template>

<script>
import Chatbot from "./components/ChatbotUI.vue";
import SideBarComponent from "./components/SideBarComponent.vue";

export default {
  components: {
    SideBarComponent,
    Chatbot,
  },
};
</script>
