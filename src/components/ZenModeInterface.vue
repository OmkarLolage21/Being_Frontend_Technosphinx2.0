<template>
    <div class="zenmode-container" :class="{ 'frozen': isFrozen }">
      <h1 class="zenmode-title">Zen Mode: Meditation</h1>
  
      <div class="form-group">
        <label for="symptom">Select Your Symptom:</label>
        <select v-model="selectedSymptom" id="symptom" @change="updateAudio">
          <option disabled value="">-- Choose a symptom --</option>
          <option v-for="symptom in symptoms" :key="symptom.id" :value="symptom.value">{{ symptom.label }}</option>
        </select>
      </div>
  
      <div class="audio-player" v-if="selectedAudio">
        <h2>{{ selectedSymptomLabel }}</h2>
        <audio controls :src="selectedAudio" @ended="handleAudioEnd" ref="audio">
          Your browser does not support the audio element.
        </audio>
      </div>
  
      <div v-if="audioEnded" class="finished-message">
        <p>Your meditation has ended. Feel free to choose another symptom.</p>
      </div>
  
      <button v-if="isFrozen" class="exit-button" @click="exitMeditation">Exit Meditation</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectedSymptom: '',
        selectedAudio: '',
        audioEnded: false,
        isFrozen: false,
        symptoms: [
          { id: 1, label: 'Anxiety', value: 'anxiety' },
          { id: 2, label: 'Stress', value: 'stress' },
          { id: 3, label: 'Depression', value: 'depression' },
          { id: 4, label: 'Insomnia', value: 'insomnia' },
        ],
      };
    },
    computed: {
      selectedSymptomLabel() {
        const symptom = this.symptoms.find(sym => sym.value === this.selectedSymptom);
        return symptom ? symptom.label : '';
      },
    },
    methods: {
      updateAudio() {
        this.audioEnded = false; // Reset audio ended status
        this.isFrozen = false; // Unfreeze on symptom change
        switch (this.selectedSymptom) {
          case 'anxiety':
            this.selectedAudio = require('@/assets/media.mp3');
            break;
          case 'stress':
            // this.selectedAudio = require('@/assets/audio/stress-meditation.mp3');
            break;
          case 'depression':
            // this.selectedAudio = require('@/assets/audio/depression-meditation.mp3');
            break;
          case 'insomnia':
            // this.selectedAudio = require('@/assets/audio/insomnia-meditation.mp3');
            break;
          default:
            this.selectedAudio = '';
        }
  
        // Freeze the screen when audio starts playing
        if (this.selectedAudio) {
          this.isFrozen = true;
          this.$nextTick(() => {
            this.$refs.audio.play();
          });
        }
      },
      handleAudioEnd() {
        this.audioEnded = true; // Set audio ended status
        this.isFrozen = false; // Unfreeze after audio ends
      },
      exitMeditation() {
        this.$refs.audio.pause();
        this.$refs.audio.currentTime = 0; // Reset audio
        this.isFrozen = false; // Unfreeze
        this.selectedSymptom = ''; // Reset symptom selection
        this.selectedAudio = ''; // Reset audio source
      },
    },
  };
  </script>
  
  <style scoped>
  .zenmode-container {
    max-width: 600px;
    margin: 50px auto;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    background-color: #ffffff;
    font-family: 'Roboto', sans-serif;
  }
  
  .zenmode-title {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  .form-group label {
    font-weight: bold;
    color: #333;
  }
  
  .form-group select {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    box-sizing: border-box;
  }
  
  .audio-player {
    margin-top: 20px;
  }
  
  .finished-message {
    margin-top: 20px;
    padding: 15px;
    background-color: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
    border-radius: 4px;
  }
  
  /* Freeze overlay style */
  .frozen {
    pointer-events: none; /* Disable all events */
    opacity: 0.5; /* Dim the background */
  }
  
  .exit-button {
    margin-top: 20px;
    padding: 10px 15px;
    background-color: #e74c3c; /* Red background */
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s;
  }
  
  .exit-button:hover {
    background-color: #c0392b; /* Darker red on hover */
  }
  </style>
  