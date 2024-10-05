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
import notelifylogo from '@/assets/notelifylogo.jpg'
import crossync from '@/assets/crossync.jpg'
import sociall from '@/assets/sociall.png'
import nn from '@/assets/nn.png'

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
          title: 'Neural Network from Scracth',
          description: 'Made an NN completely from scratch using Python, Numpy, and math. Utilizing mini-batch gradient descent. Trained on 15,000 doodle images and tested on Google dataset. Achieved confidence of 90+%.',
          image: nn,
          technologies: ['Python', 'Numpy'],
          link: 'https://github.com/arafat-ar13/NeuralNetwork'
        },
        {
          id: 3,
          title: 'Notelify',
          description: 'AI Notetaking application that turns your voice meetings into usable notes!',
          image: notelifylogo,
          technologies: ['TypeScript', 'NextJS', 'Tailwind', 'Supabase'],
          link: 'https://notelify.co'
        },
        {
          id: 4,
          title: 'Regular ToDo List',
          description: 'A full-fledged todolist web app made in Python and Django. Supports tasks, lists, attachments, notes, due dates, and an intelligent Insights feature.',
          image: todoapp,
          technologies: ['Python', 'DJango', 'JavaScript', 'JQuery', 'AJAX'],
          link: 'https://arafat13.pythonanywhere.com'
        },
        {
          id: 5,
          title: 'SociALL',
          description: 'Manage your social media posts with AI generated captions based on your images',
          image: sociall,
          technologies: ['Python', 'Flask', 'Google Gemini'],
          link: 'https://thinkedin.vercel.app/'
        },
        {
          id: 6,
          title: 'Cross Sync',
          description: 'A browser extension that syncs your browser data across multiple browsers - from Firefox to Chromium-based browsers and everything in between!',
          image: crossync,
          technologies: ['JavaScript', 'PostgreSQL', 'Heroku', 'Manifest v2'],
          link: 'https://www.crosssyncapp.co/'
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
