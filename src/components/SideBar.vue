<template>
    <div class="sidebar">
      <img src="../assets/my-avatar.jpg" alt="Avatar" class="avatar"> 
      
      <br>
  
      <h1 style="font-size: 35px;">Arafat Khan</h1>
      <p>CS @ MSU</p>
  
      <div class="description">
        <p>Who goes there! I am Arafat and I am a second-year computer science major at Michigan State University. My primary areas of focus are back-end web development and AI.</p>
      </div>
  
      <div class="footer">
        <p class="cs-msu">hello@arafatkhan.com</p>
        <div class="social-icons">
          <a href="https://github.com/arafat-ar13" target="_blank" rel="noopener noreferrer" class="icon-link">
            <i class="fab fa-github"></i>
          </a>
          <a href="https://linkedin.com/in/yourusername" target="_blank" rel="noopener noreferrer" class="icon-link">
            <i class="fab fa-linkedin"></i>
          </a>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Sidebar'
  }
  </script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400..700;1,400..700&display=swap');
  @import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css');
  
  .avatar {
    vertical-align: middle;
    align-items: center;
    width: 150px;
    height: 150px;
    border-radius: 50%;
  }
  
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    background-color: #121212;
    color: #19b8df;
    padding: 20px;
    width: 350px;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: space-between;
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
    font-family: 'Lora', serif;
  }
  
  h1 {
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  p {
    margin: 5px 0;
  }
  
  .description {
    margin-top: 20px;
    font-size: 14px;
    line-height: 1.5;
  }
  
  .footer {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    margin-top: auto;
    padding-bottom: 20px;
  }
  
  .cs-msu {
    margin-bottom: 10px;
    text-align: center;
  }
  
  .social-icons {
    display: flex;
    justify-content: center;
    width: 100%;
  }
  
  .icon-link {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50px;
    height: 50px;
    margin: 0 10px;
    border-radius: 50%;
    transition: all 0.3s ease;
  }
  
  .icon-link i {
    font-size: 30px;
    color: #95a5a6;
    transition: color 0.3s ease;
  }
  
  .icon-link:hover {
    background-color: rgba(255, 255, 255, 0.1);
  }
  
  .icon-link:hover .fa-github {
    color: #333;
  }
  
  .icon-link:hover .fa-linkedin {
    color: #0077B5;
  }
  </style>