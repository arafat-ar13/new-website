<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue'
import SideBar from './components/SideBar.vue'
import Projects from './components/Projects.vue'
import Experiences from './components/Experiences.vue'

const currentPage = ref(0)
const pages = ref([])
const showProjects = ref(false)
const showExperiences = ref(false)
const showContactIcons = ref(false)
const icons = ref([])

const handleScroll = (event) => {
  const projectsPage = pages.value[1]
  const experiencesPage = pages.value[2]
  const projectsContainer = projectsPage.querySelector('.projects-container')
  const experiencesContainer = experiencesPage.querySelector('.experiences-container')
  
  if ((currentPage.value === 1 && projectsContainer.contains(event.target)) ||
      (currentPage.value === 2 && experiencesContainer.contains(event.target))) {
    return
  }

  if (event.deltaY > 0 && currentPage.value < pages.value.length - 1) {
    currentPage.value++
  } else if (event.deltaY < 0 && currentPage.value > 0) {
    currentPage.value--
  }
  scrollToPage(currentPage.value)
}

const handleKeyDown = (event) => {
  if (event.key === 'ArrowDown' && currentPage.value < pages.value.length - 1) {
    event.preventDefault()
    currentPage.value++
    scrollToPage(currentPage.value)
  } else if (event.key === 'ArrowUp' && currentPage.value > 0) {
    event.preventDefault()
    currentPage.value--
    scrollToPage(currentPage.value)
  }
}

const scrollToPage = (pageIndex) => {
  pages.value[pageIndex].scrollIntoView({ behavior: 'smooth' })
  showProjects.value = false
  showExperiences.value = false
  showContactIcons.value = false
  
  if (pageIndex === 1) {
    setTimeout(() => {
      showProjects.value = true
    }, 1000)
  } else if (pageIndex === 2) {
    setTimeout(() => {
      showExperiences.value = true
    }, 1000)
  } else if (pageIndex === 3) {
    setTimeout(() => {
      showContactIcons.value = true
    }, 800) // Reduced delay for faster animation
  }
}

const generateRandomIcons = () => {
  const iconClasses = [
    'fas fa-laptop', 'fas fa-mouse', 'fab fa-python', 'fab fa-cuttlefish',
    'fas fa-desktop', 'fas fa-keyboard', 'fas fa-code', 'fas fa-microchip',
    'fas fa-database', 'fas fa-wifi', 'fas fa-server', 'fas fa-sitemap'
  ]
  
  const totalIcons = 28 // 7 icons per page, 4 pages
  icons.value = []

  for (let i = 0; i < totalIcons; i++) {
    const randomIcon = iconClasses[Math.floor(Math.random() * iconClasses.length)]
    const top = Math.random() * 100
    const left = Math.random() * 100
    const rotation = Math.random() * 20 // Random rotation between 0 and 20 degrees
    const page = Math.floor(i / 7) // Distribute icons evenly across 4 pages

    icons.value.push({
      class: randomIcon,
      style: {
        top: `${top}%`,
        left: `${left}%`,
        transform: `rotate(${rotation}deg)`,
        page: page
      }
    })
  }
}

onMounted(() => {
  pages.value = document.querySelectorAll('.page')
  window.addEventListener('wheel', handleScroll, { passive: false })
  window.addEventListener('keydown', handleKeyDown)
  generateRandomIcons()
})

onUnmounted(() => {
  window.removeEventListener('wheel', handleScroll)
  window.removeEventListener('keydown', handleKeyDown)
})

watch(currentPage, (newPage) => {
  if (newPage === 3) {
    showContactIcons.value = false
    setTimeout(() => {
      showContactIcons.value = true
    }, 800) // Reduced delay for faster animation
  } else {
    showContactIcons.value = false
  }
})
</script>

<template>
  <div class="app-container">
    <SideBar :currentPage="currentPage" />
    <div class="content-container">
      <div class="icon-container">
        <i v-for="(icon, index) in icons" :key="index" :class="['icon', icon.class]" :style="icon.style"></i>
      </div>
      <div class="page page-1">
        <h1>Hello there!</h1>
        <p class="navigation-instructions">
          Use <i class="fas fa-arrow-down"></i> <i class="fas fa-arrow-up"></i> to move
        </p>
      </div>
      <div class="page page-2">
        <div v-if="currentPage === 1 && !showProjects" class="project-intro">
          <h2>Look at some of my projects...</h2>
        </div>
        <Projects v-else-if="showProjects" />
      </div>
      <div class="page page-3">
        <div v-if="currentPage === 2 && !showExperiences" class="experiences-intro">
          <h2>My Experiences</h2>
        </div>
        <Experiences :showExperiences="showExperiences" />
      </div>
      <div class="page page-4">
        <h2>Contact Me</h2>
        <div class="contact-icons" :class="{ 'show-icons': currentPage === 3 }">
          <a href="https://github.com/arafat-ar13" target="_blank" rel="noopener noreferrer" class="icon-link">
            <i class="fab fa-github"></i>
          </a>
          <a href="https://www.linkedin.com/in/arafat-khan-121389tt/" target="_blank" rel="noopener noreferrer" class="icon-link">
            <i class="fab fa-linkedin"></i>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400..700;1,400..700&display=swap');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css');

h1 {
  font-family: "Lora", sans-serif;
}

.app-container {
  display: flex;
  height: 100vh;
  overflow: hidden;
}

.content-container {
  flex-grow: 1;
  margin-left: 350px; /* Adjust this to match your sidebar width */
  overflow-y: auto;
  overflow-x: hidden;
  scroll-snap-type: y mandatory;
  background-color: #121212;
  color: #ffffff;
  font-family: 'Roboto', sans-serif;
  position: relative;
}

.icon-container {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 400vh; /* Covers exactly four pages */
  pointer-events: none;
  z-index: 1;
}

.icon {
  position: absolute;
  color: rgba(128, 128, 128, 0.2);
  font-size: 24px;
}

.page {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  scroll-snap-align: start;
  position: relative;
  z-index: 2;
}

h1, h2 {
  font-size: 3rem;
  font-weight: 300;
}

.project-intro {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  text-align: center;
}

.contact-icons {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

.icon-link {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 70px;  /* Increased from 60px */
  height: 70px; /* Increased from 60px */
  margin: 0 20px;
  border-radius: 50%;
  background-color: #19b8df;
  transition: all 0.3s ease;
  transform: translateX(100vw);
}

.show-icons .icon-link {
  transform: translateX(0);
  transition: transform 0.5s ease; /* Reduced from 0.5s to 0.3s */
}

.show-icons .icon-link:nth-child(2) {
  transition-delay: 0.1s; /* Reduced from 0.1s to 0.05s */
}

.icon-link i {
  font-size: 40px; /* Increased from 30px */
  color: #121212;
}

.icon-link:hover {
  background-color: #ffffff;
  transform: scale(1.1); /* Added a slight scale effect on hover */
}

.icon-link:hover .fa-github {
  color: #333;
}

.icon-link:hover .fa-linkedin {
  color: #0077B5;
}
</style>