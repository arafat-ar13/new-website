<template>
    <div class="experiences-container">
      <div v-show="showExperiences" class="experiences-grid">
        <div 
          v-for="(experience, index) in experiences" 
          :key="experience.id" 
          class="polaroid"
          :style="{ transform: `rotate(${experience.rotation}deg)`, animationDelay: `${index * 0.5}s` }"
        >
          <img :src="experience.image" :alt="experience.title">
          <div class="polaroid-caption">
            <h3>{{ experience.title }}</h3>
            <p>{{ experience.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>

  import spartahack from '@/assets/spartahack.jpg'
  import notelify from '@/assets/notelify.jpg'
  import hiking from '@/assets/hiking.jpg'
  import ai from '@/assets/aiclub.jpg'

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
            title: 'Spartahack',
            description: 'Won Best Niche App at Spartahack 2024 as a SOLO DEVELOPER',
            image: spartahack,
            rotation: -5
          },
          {
            id: 2,
            title: 'Hiking',
            description: 'Explored beautiful trails and breathtaking views',
            image: hiking,
            rotation: 3
          },
          {
            id: 3,
            title: 'MSU AI Club App Competition',
            description: 'First place in a project app competition',
            image: notelify,
            rotation: -2
          },
          {
            id: 4,
            title: 'MSU AI Club',
            description: 'Led an image recognition AI Project with close to 100 students',
            image: ai,
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
  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  
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
    background: rgb(174, 172, 187);
    padding: 1rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 350px;
    margin: 1rem;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    opacity: 0;
    animation: fadeIn 1s forwards;
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
  

