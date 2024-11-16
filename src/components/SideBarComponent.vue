<template>
  <div class="sidebar-container">
    <!-- Sidebar Toggle Button -->
    <button
      class="sidebar-toggle-btn"
      @click="toggleSidebar"
      :class="{ 'sidebar-open': isOpen }"
    >
      <!-- <i class="fas fa-arrow-right arrow-icon" :class="{ 'rotated': isOpen }"></i> -->
      <i class="fas fa-bars"></i>
    </button>

    <!-- Sidebar -->
    <transition name="slide-sidebar">
      <div v-if="isOpen" class="sidebar">
        <h3 class="sidebar-title">Being
        </h3>
        <ul class="sidebar-list">
          <li>
            <router-link class="sidebar-link" to="/zen-mode">Zen-mode</router-link> 
          </li>
          <li>
            <router-link class="sidebar-link" to="/prescription-bill">Prescription</router-link> 
          </li>
          <li>
            <router-link class="sidebar-link" to="/book-appointment">Schedule Appointment</router-link> 
          </li>
          <li>
            <router-link class="sidebar-link" to="/doctor-connect">Doctor Connect</router-link> 
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "SideBarComponent",
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggleSidebar() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>

<style scoped>
.sidebar-container {
  position: relative;
}

/* Modern Sidebar Styling */
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 250px;
  height: 100vh;
  background-color: #1f2937; /* Dark gray background */
  color: #f9fafb; /* Light text color */
  z-index: 1000;
  padding: 20px;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.15); /* Subtle shadow */
  transition: all 0.3s ease; /* Smooth opening */
}

/* Sidebar Toggle Button */
.sidebar-toggle-btn {
  position: fixed;
  top: 20px;
  left: 20px;
  background-color: #2563eb; /* Blue background */
  color: white;
  border: none;
  padding: 12px 15px;
  border-radius: 50%;
  cursor: pointer;
  z-index: 1100;
  transition: transform 0.3s ease, left 0.3s ease;
  font-size: 16px;
  display: flex; /* Align items in a row */
  align-items: center; /* Center the icon vertically */
}

/* Arrow Icon */
.arrow-icon {
  margin-right: 5px; /* Space between the arrow and the menu icon */
  transition: transform 0.3s ease; /* Smooth rotation */
}

.arrow-icon.rotated {
  transform: rotate(90deg); /* Rotate arrow when sidebar is open */
}

.sidebar-toggle-btn:hover {
  background-color: #1e40af; /* Darker blue on hover */
}

.sidebar-toggle-btn.sidebar-open {
  transform: rotate(90deg); /* Rotate the button when sidebar is open */
  left: 270px; /* Adjust button position when sidebar is open */
}

/* Sidebar Title */
.sidebar-title {
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 20px;
  color: #ffffff;
  text-transform: uppercase;
}

/* Sidebar List */
.sidebar-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.sidebar-list li {
  margin-bottom: 15px;
}

/* Sidebar Links */
.sidebar-link {
  display: block;
  padding: 10px 15px;
  background-color: #374151; /* Medium gray for items */
  color: #f9fafb;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 500;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.sidebar-link:hover {
  background-color: #2563eb; /* Highlight on hover */
  color: white; /* Ensure text is visible on hover */
}

/* Slide animations */
.slide-sidebar-enter-active,
.slide-sidebar-leave-active {
  transition: transform 0.3s ease;
}

.slide-sidebar-enter,
.slide-sidebar-leave-to {
  transform: translateX(-100%);
}
</style>
