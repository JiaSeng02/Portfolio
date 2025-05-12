<template>
  <div class="about-me-container">
    <div class="about-me">
      <header class="header">
        <h1>About Me</h1>
        <img :src="profileImage" alt="Profile Picture" class="profile-img" />
        <p class="tagline">Get to know me better</p>
        <div class="resume-download">
          <button @click="downloadResume" class="download-btn">
            Download My Resume
          </button>
        </div>
      </header>

      <main class="content-scrollable">
        <section class="intro">
          <div class="profile">
            <h2>Hello, I'm Jia Seng</h2>
            <p class="profession">Frontend Developer</p>
          </div>
          <div class="bio">
            <p>
              Welcome to my personal space! I'm passionate about creating
              beautiful, functional websites. With my studies life in UTAR, I've
              developed skills in HTML, React-native, and JavaScript.
            </p>
            <p>
              When I'm not coding, you can find me singing or playing
              basketball.
            </p>
          </div>
        </section>

        <section class="details">
          <div class="skills">
            <h3>My Skills</h3>
            <ul>
              <li v-for="skill in skills" :key="skill">{{ skill }}</li>
            </ul>
          </div>

          <div class="internship">
            <h3>Internship</h3>
            <div v-for="job in internship" :key="job.title" class="job">
              <h4>{{ job.title }}</h4>
              <p class="company">{{ job.company }} | {{ job.duration }}</p>
              <p>{{ job.description }}</p>
            </div>
          </div>

          <div class="education">
            <h3>Education</h3>
            <div v-for="edu in education" :key="edu.degree" class="degree">
              <h4>{{ edu.degree }}</h4>
              <p class="institution">{{ edu.institution }} | {{ edu.year }}</p>
            </div>
          </div>
        </section>

        <section class="contact">
          <h3>Let's Connect</h3>
          <div class="social-links">
            <a
              v-for="link in socialLinks"
              :href="link.url"
              :key="link.name"
              target="_blank"
              class="social-link"
            >
              <i :class="link.icon" v-if="link.icon"></i>
              {{ link.name }}
            </a>
          </div>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "AboutMe",
  data() {
    return {
      profileImage: require("@/assets/Profile.jpg"), // Update this path
      skills: ["HTML", "Vue.js", "CSS", "Laravel", "Java", "Git"],
      internship: [
        {
          title: "Intern",
          company: "Genetec Technology Berhad",
          duration: "October 2023",
          description:
            "Exploring machine automation with new graphical programming language Ladder Logic",
        },
      ],
      education: [
        {
          degree: "Bachelor of Software Engineering",
          institution: "Universiti Tunku Abdul Rahman",
          year: "2022-2025",
        },
      ],
      socialLinks: [
        {
          name: "LinkedIn",
          url: "https://www.linkedin.com/in/jiaseng2002/",
          icon: "fab fa-linkedin",
        },
        {
          name: "GitHub",
          url: "https://github.com/JiaSeng02",
          icon: "fab fa-github",
        },
        {
          name: "Email",
          url: "mailto:jiaseng02@gmail.com",
          icon: "fas fa-envelope",
        },
      ],
    };
  },
  methods: {
    downloadResume() {
      const link = document.createElement("a");
      link.href = "@/assets/LeeJiaSeng_Resume.pdf";
      link.download = "JiaSeng_Resume.pdf";
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },
  },
};
</script>

<style scoped>
.about-me-container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.about-me {
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem;
  font-family: "Arial", sans-serif;
  color: #333;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.header {
  text-align: center;
  margin-bottom: 1rem;
}

.header h1 {
  font-size: 2.5rem;
  color: #2c3e50;
  margin-bottom: 0.5rem;
}

.tagline {
  font-size: 1.2rem;
  color: #7f8c8d;
  margin-bottom: 1rem;
}

.resume-download {
  margin: 1rem 0 2rem;
}

.download-btn {
  background: #3498db;
  color: white;
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.3s;
}

.download-btn:hover {
  background: #2980b9;
}

.content-scrollable {
  overflow-y: auto;
  flex: 1;
  padding: 1rem 0;
}

.intro {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  align-items: center;
  margin-bottom: 2rem;
}

.profile {
  text-align: center;
  flex: 1;
  min-width: 250px;
}

.profile-img {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  object-fit: cover;
  border: 5px solid #ecf0f1;
}

.profile h2 {
  margin-top: 1rem;
  color: #2c3e50;
}

.profession {
  color: #3498db;
  font-weight: bold;
  margin-bottom: 1rem;
}

.bio {
  flex: 2;
  min-width: 300px;
  line-height: 1.6;
}

.details {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

h3 {
  color: #2c3e50;
  border-bottom: 2px solid #3498db;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
}

.job,
.degree {
  margin-bottom: 1.5rem;
}

.company,
.institution {
  color: #7f8c8d;
  font-style: italic;
}

.skills ul {
  list-style-type: none;
  padding: 0;
}

.skills li {
  background: #ecf0f1;
  margin-bottom: 0.5rem;
  padding: 0.5rem 1rem;
  border-radius: 4px;
}

.contact {
  text-align: center;
  margin-top: 2rem;
  padding-bottom: 2rem;
}

.social-links {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.social-link {
  color: white;
  background: #3498db;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  text-decoration: none;
  transition: background 0.3s;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.social-link:hover {
  background: #2980b9;
}

@media (max-width: 768px) {
  .intro {
    flex-direction: column;
  }

  .profile,
  .bio {
    flex: none;
    width: 100%;
  }

  .content-scrollable {
    padding: 1rem;
  }
}

/* Scrollbar styling */
.content-scrollable::-webkit-scrollbar {
  width: 8px;
}

.content-scrollable::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 10px;
}

.content-scrollable::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 10px;
}

.content-scrollable::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
