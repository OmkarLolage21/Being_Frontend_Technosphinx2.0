<template>
    <div class="appointment-container">
      <h1 class="appointment-title">Book an Appointment</h1>
      <form @submit.prevent="submitForm" class="appointment-form">
        <div class="form-group">
          <label for="name">Full Name:</label>
          <input type="text" v-model="appointmentData.name" id="name" required />
        </div>
  
        <div class="form-group">
          <label for="email">Email:</label>
          <input type="email" v-model="appointmentData.email" id="email" required />
        </div>
  
        <div class="form-group">
          <label for="phone">Phone Number:</label>
          <input type="tel" v-model="appointmentData.phone" id="phone" required />
        </div>
  
        <div class="form-group">
          <label for="date">Date:</label>
          <input type="date" v-model="appointmentData.date" id="date" required />
        </div>
  
        <div class="form-group">
          <label for="time">Time:</label>
          <select v-model="appointmentData.time" id="time" required>
            <option disabled value="">Select a time</option>
            <option v-for="time in availableTimes" :key="time" :value="time">{{ time }}</option>
          </select>
        </div>
  
        <div class="form-group">
          <label for="doctor">Select Doctor:</label>
          <select v-model="appointmentData.doctor" id="doctor" required>
            <option disabled value="">Select a doctor</option>
            <option v-for="doctor in doctors" :key="doctor.id" :value="doctor.name">{{ doctor.name }}</option>
          </select>
        </div>
  
        <button type="submit" class="submit-btn">Book Appointment</button>
      </form>
  
      <div v-if="confirmationMessage" class="confirmation-message">
        <p>{{ confirmationMessage }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        appointmentData: {
          name: '',
          email: '',
          phone: '',
          date: '',
          time: '',
          doctor: '',
        },
        doctors: [
          { id: 1, name: 'Dr. Smith - Cardiologist' },
          { id: 2, name: 'Dr. Johnson - Dermatologist' },
          { id: 3, name: 'Dr. Lee - Pediatrician' },
        ],
        availableTimes: [
          '09:00 AM',
          '10:00 AM',
          '11:00 AM',
          '01:00 PM',
          '02:00 PM',
          '03:00 PM',
        ],
        confirmationMessage: '',
      };
    },
    methods: {
      submitForm() {
        // Here you would typically send the data to your server or API
        this.confirmationMessage = `Appointment booked successfully for ${this.appointmentData.name} on ${this.appointmentData.date} at ${this.appointmentData.time} with ${this.appointmentData.doctor}.`;
        this.resetForm();
      },
      resetForm() {
        this.appointmentData = {
          name: '',
          email: '',
          phone: '',
          date: '',
          time: '',
          doctor: '',
        };
      },
    },
  };
  </script>
  
  <style scoped>
  .appointment-container {
    max-width: 600px;
    margin: 50px auto;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    background-color: #ffffff;
    font-family: 'Roboto', sans-serif;
  }
  
  .appointment-title {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
  }
  
  .appointment-form {
    display: flex;
    flex-direction: column;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  .form-group label {
    font-weight: bold;
    color: #333;
  }
  
  .form-group input,
  .form-group select {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    box-sizing: border-box;
  }
  
  .form-group input:focus,
  .form-group select:focus {
    border-color: #007bff;
    outline: none;
  }
  
  .submit-btn {
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
  }
  
  .submit-btn:hover {
    background-color: #0056b3;
  }
  
  .confirmation-message {
    margin-top: 20px;
    padding: 15px;
    background-color: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
    border-radius: 4px;
  }
  </style>
  