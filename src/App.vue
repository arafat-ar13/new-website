<script setup>
import { ref, onMounted } from 'vue'
import SideBar from './components/SideBar.vue'
import Projects from './components/Projects.vue'

const currentPage = ref(0)
const pages = ref([])
const showProjects = ref(false)
const icons = ref([])

const handleScroll = (event) => {
  const projectsPage = pages.value[1]
  const projectsContainer = projectsPage.querySelector('.projects-container')
  
  if (currentPage.value === 1 && projectsContainer.contains(event.target)) {
    return
  }

  if (event.deltaY > 0 && currentPage.value < pages.value.length - 1) {
    currentPage.value++
  } else if (event.deltaY < 0 && currentPage.value > 0) {
    currentPage.value--
  }
  scrollToPage(currentPage.value)
}

const scrollToPage = (pageIndex) => {
  pages.value[pageIndex].scrollIntoView({ behavior: 'smooth' })
  if (pageIndex === 1) {
    setTimeout(() => {
      showProjects.value = true
    }, 3000)
  } else {
    showProjects.value = false
  }
}

const generateRandomIcons = () => {
  const iconClasses = [
    'fas fa-laptop', 'fas fa-mouse', 'fab fa-python', 'fab fa-cuttlefish',
    'fas fa-desktop', 'fas fa-keyboard', 'fas fa-code', 'fas fa-microchip',
    'fas fa-database', 'fas fa-wifi', 'fas fa-server', 'fas fa-sitemap'
  ]
  
  const totalIcons = 14 // 7 icons per page, 2 pages
  icons.value = []

  for (let i = 0; i < totalIcons; i++) {
    const randomIcon = iconClasses[Math.floor(Math.random() * iconClasses.length)]
    const top = Math.random() * 100
    const left = Math.random() * 100
    const rotation = Math.random() * 20 // Random rotation between 0 and 20 degrees
    const page = i < 7 ? 0 : 1 // First 7 icons on page 0, rest on page 1

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
  generateRandomIcons()
})
</script>

<template>
  <div class="app-container">
    <SideBar />
    <div class="content-container">
      <div class="icon-container">
        <i v-for="(icon, index) in icons" :key="index" :class="['icon', icon.class]" :style="icon.style"></i>
      </div>
      <div class="page page-1">
        <h1>Hello there!</h1>
      </div>
      <div class="page page-2">
        <div v-if="currentPage === 1 && !showProjects" class="project-intro">
          <h2>Now get ready for some quality projects...</h2>
        </div>
        <Projects v-else-if="showProjects" />
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
  height: 200vh; /* Covers exactly two pages */
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
</style>