<template>
  <div class="prescription-uploader">
    <input
      type="file"
      @change="handleFileUpload"
      accept="image/*"
      ref="fileInput"
      style="display: none"
    />
    <button @click="$refs.fileInput.click()" class="upload-btn">
      Upload Prescription
    </button>

    <div v-if="isLoading" class="loading">Processing prescription...</div>
    <div v-if="error" class="error">{{ error }}</div>

    <div v-if="cart.length > 0" class="cart">
      <h3>Cart</h3>
      <div class="cart-items">
        <div v-for="(item, index) in cart" :key="index" class="cart-item">
          <img :src="item.image" alt="Medicine Image" class="item-image" />
          <div>
            <h4 class="item-name">{{ item.name }}</h4>
            <p class="item-quantity">Quantity: {{ item.quantity }}</p>
          </div>
        </div>
      </div>
      <button @click="proceedToBilling" class="billing-btn">Proceed to Billing</button>
      <button @click="generateInvoice" class="invoice-btn">Generate Invoice</button>
    </div>
  </div>
</template>

<script>
import jsPDF from 'jspdf'; // Import jsPDF for generating PDF

export default {
  name: 'PrescriptionBill',
  data() {
    return {
      isLoading: false,
      error: null,
      cart: [],
    };
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (!file) return;

      this.isLoading = true;
      this.error = null;

      // Simulate image processing and text extraction
      setTimeout(() => {
        this.processPrescription(file);
      }, 2000);
    },
    processPrescription() {
      // Simulated extraction of medicine information with image paths
      const mockExtractedData = [
        { name: 'Aspirin', quantity: 30, image: require('@/assets/asp.jpg') },
        { name: 'Lisinopril', quantity: 60, image: require('@/assets/asp.jpg') },
        { name: 'Metformin', quantity: 90, image: require('@/assets/asp.jpg') },
      ];

      this.addToCart(mockExtractedData);
      this.isLoading = false;
    },
    addToCart(medicines) {
      this.cart = medicines;
    },
    proceedToBilling() {
      console.log('Proceeding to billing with cart:', this.cart);
      this.$emit('proceed-to-billing', this.cart);
    },
    generateInvoice() {
      const doc = new jsPDF();
      doc.text("Prescription Invoice", 20, 20);
      doc.text("Medicines:", 20, 30);

      let yOffset = 40;
      this.cart.forEach((item) => {
        doc.text(`${item.name} - Quantity: ${item.quantity}`, 20, yOffset);
        yOffset += 10; // Increment yOffset for each item
      });

      doc.save("invoice.pdf");
    },
  },
};
</script>

<style scoped>
.prescription-uploader {
  max-width: 600px; /* Increased max width for a more spacious layout */
  margin: 50px auto; /* Center horizontally and add margin */
  padding: 20px;
  border-radius: 8px;
  background-color: #f9f9f9; /* Light background for a clean look */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1); /* Soft shadow */
}

.upload-btn, .billing-btn, .invoice-btn {
  background-color: #28a745; /* Green primary button color */
  color: white;
  border: none;
  padding: 12px 15px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  margin-bottom: 10px;
  width: 100%; /* Full width for buttons */
  transition: background-color 0.3s, transform 0.3s;
}

.upload-btn:hover, .billing-btn:hover, .invoice-btn:hover {
  background-color: #218838; /* Darker green on hover */
  transform: translateY(-1px); /* Slight lift effect */
}

.loading, .error {
  margin-top: 10px;
  font-style: italic;
}

.error {
  color: red;
}

.cart {
  margin-top: 20px;
}

.cart-items {
  display: flex;
  flex-direction: column;
  gap: 10px; /* Space between items */
}

.cart-item {
  display: flex; /* Flexbox for image and text */
  align-items: center; /* Center items vertically */
  background-color: white; /* White background for cart items */
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* Light shadow for cards */
  transition: transform 0.2s;
}

.cart-item:hover {
  transform: translateY(-2px); /* Lift effect on hover */
}

.item-image {
  width: 60px; /* Fixed width for images */
  height: 60px; /* Fixed height for images */
  border-radius: 5px; /* Rounded corners */
  margin-right: 15px; /* Space between image and text */
}

.item-name {
  margin: 0;
  font-weight: bold;
  color: #333;
}

.item-quantity {
  margin: 0;
  color: #666; /* Lighter color for quantity */
}
</style>
