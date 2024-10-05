<template>
  <div class="projects-container">
    <div class="projects-grid">
      <a 
        v-for="(project, index) in projects" 
        :key="project.id" 
        :href="project.link" 
        target="_blank" 
        rel="noopener noreferrer"
        class="project-card" 
        :style="{ animationDelay: `${index * 0.3}s` }"
      >
        <img :src="project.image" :alt="project.title" class="project-image">
        <div class="project-content">
          <h2 class="project-title">{{ project.title }}</h2>
          <p class="project-description">{{ project.description }}</p>
        </div>
        <div class="project-footer">
          <span v-for="tech in project.technologies" :key="tech" class="tech-tag">
            {{ tech }}
          </span>
        </div>
      </a>
    </div>
  </div>
</template>

<script>

import languagepp from '@/assets/languagepp.png';
import todoapp from '@/assets/todoapp.png';

export default {
  name: 'Projects',
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'Language++',
          description: 'An AI Language Pronunciation Trainer. Gets the users voice data in different languages and gives speech feedback on how to improve the pronunciations',
          image: languagepp,
          technologies: ['Azure Speech AI', 'Streamlit', 'GPT 4-0', 'Python'],
          link: 'https://languageplusplus.streamlit.app/'
        },
        {
          id: 2,
          title: 'Project 2',
          description: 'Project 2 is an innovative mobile app that helps users track their fitness goals.',
          image: '/path/to/project2-image.jpg',
          technologies: ['React Native', 'Firebase', 'Redux'],
          link: 'https://example.com/project2'
        },
        {
          id: 3,
          title: 'Regular ToDo List',
          description: 'A full-fledged todolist web app made in Python and Django. Supports tasks, lists, attachments, notes, due dates, and an intelligent Insights feature.',
          image: todoapp,
          technologies: ['Python', 'DJango', 'JavaScript', 'JQuery', 'AJAX'],
          link: 'https://arafat13.pythonanywhere.com'
        },
        {
          id: 4,
          title: 'Project 4',
          description: 'An e-commerce platform built with microservices architecture for high scalability.',
          image: '/path/to/project4-image.jpg',
          technologies: ['Java', 'Spring Boot', 'Docker'],
          link: 'https://example.com/project4'
        },
        {
          id: 5,
          title: 'Project 5',
          description: 'A real-time chat application with end-to-end encryption for secure communication.',
          image: '/path/to/project5-image.jpg',
          technologies: ['Socket.io', 'Express.js', 'React'],
          link: 'https://example.com/project5'
        },
        {
          id: 6,
          title: 'Project 6',
          description: 'An AI-powered image recognition system for identifying plant species.',
          image: '/path/to/project6-image.jpg',
          technologies: ['Python', 'OpenCV', 'Keras'],
          link: 'https://example.com/project6'
        }
      ]
    }
  }
}
</script>

<style scoped>
.projects-container {
  padding: 2rem;
  margin-left: 45px;
  height: 100vh;
  overflow-y: auto;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
  max-width: 1000px;
  margin: 0 auto;
}

.project-card {
  background-color: #1e1e1e;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  width: 400px;
  opacity: 0;
  animation: fadeIn 0.5s ease forwards;
  text-decoration: none;
  color: inherit;
  display: block;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.project-card:hover {
  transform: translateY(-5px) scale(1.03);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2), 0 0 15px rgba(173, 216, 230, 0.5); /* Light blue glow */
}



.project-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image {
  transform: scale(1.05);
}

.project-content {
  padding: 1.5rem;
}

.project-title {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
  color: #ffffff;
}

.project-description {
  font-size: 1rem;
  color: #b0b0b0;
  margin-bottom: 1rem;
}

.project-footer {
  padding: 1rem 1.5rem;
  background-color: #252525;
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background-color: #3a3a3a;
  color: #ffffff;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  font-size: 0.8rem;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.project-card:hover .tech-tag {
  background-color: #ffff99; /* Light yellow background */
  color: #000000; /* Change text color to black for better contrast */
}

</style>
