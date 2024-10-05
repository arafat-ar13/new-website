<template>
    <div class="experiences-container">
      <div v-show="showExperiences" class="experiences-grid">
        <div 
          v-for="experience in experiences" 
          :key="experience.id" 
          class="polaroid"
          :style="{ transform: `rotate(${experience.rotation}deg)` }"
        >
          <img src="../assets/my-avatar.jpg" :alt="experience.title">
          <div class="polaroid-caption">
            <h3>{{ experience.title }}</h3>
            <p>{{ experience.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Experiences',
    props: {
      showExperiences: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        experiences: [
          {
            id: 1,
            title: 'Spartahack Winner',
            description: 'Won the hackathon with an innovative project',
            image: '/path/to/spartahack-image.jpg',
            rotation: -5
          },
          {
            id: 2,
            title: 'Hiking Adventure',
            description: 'Explored beautiful trails and breathtaking views',
            image: '/path/to/hiking-image.jpg',
            rotation: 3
          },
          {
            id: 3,
            title: 'App Competition Winner',
            description: 'First place in a project app competition',
            image: '/path/to/app-competition-image.jpg',
            rotation: -2
          },
          {
            id: 4,
            title: 'AI Club Leadership',
            description: 'Led an AI club, organizing workshops and events',
            image: '/path/to/ai-club-image.jpg',
            rotation: 4
          }
        ]
      }
    },
    watch: {
      showExperiences(newValue) {
        console.log('showExperiences changed:', newValue);
      }
    },
    mounted() {
      console.log('Experiences component mounted');
    }
  }
  </script>
  
  <style scoped>
  .experiences-container {
    height: 100vh;
    width: 100%;
    position: relative;
    overflow: hidden;
  }
  
  .experiences-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
    height: 100%;
    padding: 2rem;
  }
  
  .polaroid {
    background: white;
    padding: 1rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 250px;
    margin: 1rem;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .polaroid:hover {
    transform: scale(1.05) !important;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }
  
  .polaroid img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
  
  .polaroid-caption {
    margin-top: 1rem;
    text-align: center;
    color: #333;
  }
  
  .polaroid-caption h3 {
    margin-bottom: 0.5rem;
  }
  
  .polaroid-caption p {
    font-size: 0.9rem;
  }
  </style>