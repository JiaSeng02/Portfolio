<template>
  <div class="portfolio-container" ref="container" @wheel="handleWheel">
    <!-- Home Section -->
    <section class="page home-page" :class="{ active: currentPage === 0 }">
      <div class="hero-content">
        <div class="profile-container">
          <div class="text-content">
            <h2 class="animated-text">Hello, I'm</h2>
            <h1 class="name-title">Lee Jia Seng</h1>
            <h3 class="job-title">Frontend Developer</h3>
            <p class="bio">
              I am a fresh graduate from Universiti Tunku Abdul Rahman(UTAR)
              with Degree in Bachelor of Software Engineerig. I am aspiring
              Front-end Developer with prior experience building small projects.
              Good foundation in HTML, CSS, and JavaScript, with a strong
              eagerness to learn and improve. Passionate about developing
              responsive and user friendly web applications. Looking for an
              opportunity to enhance my skills and grow as a developer in a
              professional setting.
            </p>
          </div>

          <div class="avatar-wrapper">
            <img src="Profile.jpg" alt="LeeJiaSeng" class="avatar-image" />
          </div>
        </div>
      </div>
      <div @click="goToPage(1)" class="scroll-indicator">
        <span>Learn more about me</span>
        <Icon type="arrowDown" />
      </div>
    </section>

    <!-- About Section -->
    <section class="page about-page" :class="{ active: currentPage === 1 }">
      <div class="content">
        <h2 class="section-title">My Background</h2>
        <div class="about-content">
          <div class="education">
            <h3>Education</h3>
            <p>Degree in Bachelor of Software Engineering</p>
            <p>Universiti Tunku Abdul Rahman (UTAR), 2022-2025</p>
            <p>CGPA: 2.9246</p>
          </div>
          <div class="experience">
            <h3>Internship</h3>
            <p>Genetec Technology Berhad (October 2023)</p>
          </div>
        </div>
      </div>
      <div class="page-controls">
        <button @click="goToPage(0)" class="nav-button">
          <Icon type="arrowUp" /> Home
        </button>
        <button @click="goToPage(2)" class="nav-button">
          My Skills <Icon type="arrowDown" />
        </button>
      </div>
    </section>

    <!-- Skills Section -->
    <section class="page skills-page" :class="{ active: currentPage === 2 }">
      <div class="content">
        <h2 class="section-title">My Skills</h2>

        <div class="skills-container">
          <!-- Technical Skills -->
          <div class="skills-column">
            <h3 class="skills-header">Technical Skills</h3>
            <div
              class="skill-item"
              v-for="skill in technicalSkills"
              :key="skill.name"
            >
              <div class="skill-info">
                <span class="skill-name">{{ skill.name }}</span>
                <span class="skill-percent">{{ skill.percent }}%</span>
              </div>
              <div class="skill-bar">
                <div
                  class="skill-progress"
                  :style="{ width: skill.percent + '%' }"
                ></div>
              </div>
            </div>
          </div>

          <!-- Soft Skills -->
          <div class="skills-column">
            <h3 class="skills-header">Soft Skills</h3>
            <div
              class="skill-item"
              v-for="skill in softSkills"
              :key="skill.name"
            >
              <div class="skill-info">
                <span class="skill-name">{{ skill.name }}</span>
                <div class="star-rating">
                  <span
                    v-for="n in 5"
                    :key="n"
                    :class="{ 'star-filled': n <= skill.rating }"
                    >★</span
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div @click="goToPage(1)" class="scroll-indicator">
        <Icon type="arrowUp" />
        <span>Back to About</span>
      </div>
    </section>

    <!-- Page Indicator -->
    <div class="page-indicator">
      <div
        v-for="(page, index) in 3"
        :key="index"
        :class="{ active: currentPage === index }"
        @click="goToPage(index)"
      ></div>
    </div>
  </div>
</template>

<script>
import Icon from "@/components/Icon";

export default {
  components: {
    Icon,
  },
  data() {
    return {
      currentPage: 0,
      isScrolling: false,
      technicalSkills: [
        { name: "HTML", percent: 90 },
        { name: "CSS", percent: 85 },
        { name: "JavaScript", percent: 60 },
        { name: "Git", percent: 85 },
        { name: "MySQL", percent: 80 },
        { name: "Vue.js", percent: 35 },
        { name: "Java", percent: 75 },
        { name: "C++", percent: 75 },
        { name: "Laravel", percent: 70 },
      ],
      softSkills: [
        { name: "Communication", rating: 4 },
        { name: "Teamwork", rating: 4 },
        { name: "Problem Solving", rating: 4 },
        { name: "Adaptability", rating: 4 },
        { name: "Creativity", rating: 3 },
      ],
    };
  },
  methods: {
    goToPage(pageIndex) {
      if (this.isScrolling) return;
      this.isScrolling = true;
      this.currentPage = pageIndex;
      setTimeout(() => {
        this.isScrolling = false;
      }, 1000);
    },
    handleWheel(e) {
      if (this.isScrolling) return;

      if (e.deltaY > 50 && this.currentPage < 2) {
        this.goToPage(this.currentPage + 1);
      } else if (e.deltaY < -50 && this.currentPage > 0) {
        this.goToPage(this.currentPage - 1);
      }
    },
  },
};
</script>

<style lang="less" scoped>
@import "~@/styles/var.less";

.portfolio-container {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  position: relative;
  scroll-behavior: smooth;
}

.page {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  padding: 2rem;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: transform 0.8s ease-in-out, opacity 0.8s ease;
  transform: translateY(100%);
  opacity: 0;

  &.active {
    transform: translateY(0);
    opacity: 1;
    z-index: 1;
  }

  .content {
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;
  }
}

.home-page {
  background: linear-gradient(135deg, #2c1e5f 0%, #433969 100%);
  color: white;

  .hero-content {
    max-width: 800px;
    margin: 0 auto;

    .profile-container {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 4rem;
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 2rem;
      @media (max-width: 768px) {
        flex-direction: column;
        gap: 2rem;
        text-align: center;
      }
    }

    .avatar-wrapper {
      flex-shrink: 0;
      width: 250px;
      height: 250px;
      border-radius: 50%;
      overflow: hidden;
      border: 5px solid #00d1b2;
      box-shadow: 0 0 20px rgba(0, 209, 178, 0.5);
      animation: fadeIn 1s ease-out 0.3s forwards;
      opacity: 0;

      .avatar-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform 0.3s ease;
        object-position: center center;
      }
    }

    .text-content {
      max-width: 600px;
    }

    .animated-text {
      animation: fadeInUp 1s ease-out;
    }

    .name-title {
      font-size: 3.5rem;
      margin: 1rem 0;
      color: #00d1b2;
      text-shadow: 0 0 10px rgba(0, 209, 178, 0.5);
      animation: fadeIn 1s ease-out 0.3s forwards;
      opacity: 0;
    }

    .job-title {
      font-size: 2rem;
      margin: 0.5rem 0 2rem;
      animation: fadeIn 1s ease-out 0.6s forwards;
      opacity: 0;
    }

    .bio {
      font-size: 1.2rem;
      line-height: 1.6;
      max-width: 600px;
      margin: 0 auto 3rem;
      animation: fadeIn 1s ease-out 0.9s forwards;
      opacity: 0;
    }
  }

  .scroll-indicator {
    position: absolute;
    bottom: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    color: white;
    cursor: pointer;
    animation: bounce 2s infinite;

    span {
      margin-bottom: 0.5rem;
    }
  }
}

.about-page {
  background-color: #f8f9fa;
  color: #333;

  .section-title {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    color: #2c3e50;
  }

  .about-content {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    gap: 2rem;

    > div {
      flex: 1;
      min-width: 300px;
      background: white;
      padding: 2rem;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

      h3 {
        color: #00d1b2;
        margin-bottom: 1rem;
        font-size: 1.5rem;
      }

      p {
        margin: 0.5rem 0;
        line-height: 1.6;
      }
    }
  }

  .page-controls {
    display: flex;
    justify-content: space-between;
    width: 100%;
    max-width: 1200px;
    margin-top: 2rem;

    .nav-button {
      background: #00d1b2;
      color: white;
      border: none;
      padding: 0.8rem 1.5rem;
      border-radius: 4px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      transition: all 0.3s ease;

      &:hover {
        background: darken(#00d1b2, 10%);
        transform: translateY(-2px);
      }
    }
  }
}

.skills-page {
  background-color: #2c3e50;
  color: white;
  padding: 2rem;

  .section-title {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    color: #00d1b2;
  }

  .skills-container {
    display: flex;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
    gap: 3rem;

    @media (max-width: 768px) {
      flex-direction: column;
      gap: 2rem;
    }
  }

  .skills-column {
    flex: 1;
    background: rgba(255, 255, 255, 0.1);
    padding: 2rem;
    border-radius: 8px;
    backdrop-filter: blur(5px);
  }

  .skills-header {
    color: #00d1b2;
    font-size: 1.5rem;
    margin-bottom: 2rem;
    text-align: center;
    border-bottom: 2px solid #00d1b2;
    padding-bottom: 0.5rem;
  }

  .skill-item {
    margin-bottom: 1.5rem;
  }

  .skill-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.5rem;
  }

  .skill-name {
    font-weight: 500;
  }

  .skill-percent {
    color: #00d1b2;
  }

  .skill-bar {
    height: 10px;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 5px;
    overflow: hidden;
  }

  .skill-progress {
    height: 100%;
    background: linear-gradient(90deg, #00d1b2, #00b3a7);
    border-radius: 5px;
    transition: width 1s ease-out;
  }

  .star-rating {
    color: #ccc;
    font-size: 1.2rem;
    letter-spacing: 2px;
  }

  .star-filled {
    color: #ffd700;
  }

  .scroll-indicator {
    position: absolute;
    top: 2rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: white;
    cursor: pointer;
  }
}

.page-indicator {
  position: fixed;
  right: 2rem;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 1rem;
  z-index: 100;

  div {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.5);
    cursor: pointer;
    transition: all 0.3s ease;

    &.active {
      background-color: #00d1b2;
      transform: scale(1.3);
    }

    &:hover {
      transform: scale(1.2);
    }
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounce {
  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}
</style>
