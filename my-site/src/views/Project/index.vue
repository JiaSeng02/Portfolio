<template>
  <div class="projects-page">
    <main class="projects-container">
      <h2 class="section-title">My Projects</h2>

      <div class="projects-grid">
        <div
          class="project-card"
          v-for="(project, index) in projects"
          :key="index"
          @click="openModal(project)"
        >
          <div
            class="project-header"
            :style="{ backgroundImage: `url(${project.image})` }"
          >
            <h3>{{ project.title }}</h3>
          </div>
          <div class="project-content">
            <p>{{ project.description }}</p>
            <div class="project-tags">
              <span v-for="(tag, tagIndex) in project.tags" :key="tagIndex">{{
                tag
              }}</span>
            </div>
            <a href="#" class="project-link">View Project →</a>
          </div>
        </div>
      </div>

      <!-- Project Modal -->
      <div class="modal-overlay" v-if="selectedProject" @click="closeModal">
        <div class="project-modal" @click.stop>
          <button class="close-btn" @click="closeModal">×</button>
          <div
            class="modal-header"
            :style="{ backgroundImage: `url(${selectedProject.image})` }"
          ></div>
          <div class="modal-content">
            <h3>{{ selectedProject.title }}</h3>
            <p>{{ selectedProject.description }}</p>
            <div class="modal-tags">
              <span
                v-for="(tag, tagIndex) in selectedProject.tags"
                :key="tagIndex"
                >{{ tag }}</span
              >
            </div>
            <button
              @click="playVideo(selectedProject.video)"
              class="modal-link"
            >
              Play Project Video →
            </button>
          </div>
        </div>
      </div>

      <!-- Video Player Modal -->
      <div
        class="video-overlay"
        v-if="showVideoPlayer"
        @click="closeVideoPlayer"
      >
        <div class="video-player" @click.stop>
          <button class="close-btn" @click="closeVideoPlayer">×</button>
          <video controls autoplay ref="videoPlayer">
            <source :src="currentVideo" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "ProjectsPage",
  data() {
    return {
      selectedProject: null,
      showVideoPlayer: false,
      currentVideo: "",
      projects: [
        {
          title: "Lyrics Player",
          description: "A web music player",
          tags: ["Music Player", "HTML", "JavaScript"],
          image:
            "https://images.unsplash.com/photo-1470225620780-dba8ba36b745?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          video: "MusicLyrics.mp4",
        },
        {
          title: "DeliveryApp",
          description: "A Web-Based Drinks Delivery App",
          tags: ["Mobile App", "E-commerce", "HTML"],
          image:
            "https://images.unsplash.com/photo-1555396273-367ea4eb4db5?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          video: "DeliveryApp.mp4",
        },
        {
          title: "UniApp",
          description: "This is an UniApp using HBuilder",
          tags: ["Mobile App", "Vue.js", "UniApp"],
          image:
            "https://images.unsplash.com/photo-1555774698-0b77e0d5fac6?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
          video: "Uni-App.mp4",
        },
      ],
    };
  },
  methods: {
    openModal(project) {
      this.selectedProject = project;
      document.body.style.overflow = "hidden";
    },
    closeModal() {
      this.selectedProject = null;
      document.body.style.overflow = "auto";
    },
    playVideo(videoUrl) {
      this.currentVideo = videoUrl;
      this.showVideoPlayer = true;
      document.body.style.overflow = "hidden";

      // Close the project modal
      this.closeModal();

      // Auto-play when the video player opens
      this.$nextTick(() => {
        this.$refs.videoPlayer.play();
      });
    },
    closeVideoPlayer() {
      this.showVideoPlayer = false;
      document.body.style.overflow = "auto";

      // Pause the video when closing
      if (this.$refs.videoPlayer) {
        this.$refs.videoPlayer.pause();
      }
    },
  },
};
</script>

<style scoped>
.projects-page {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  color: #333;
}

.section-title {
  font-size: 1.8rem;
  margin-bottom: 2rem;
  color: #2c3e50;
  text-align: center;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
}

.project-card {
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.3s, box-shadow 0.3s;
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.project-header {
  height: 180px;
  background-size: cover;
  background-position: center;
  color: white;
  padding: 1.5rem;
  position: relative;
  display: flex;
  align-items: flex-end;
}

.project-header::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.7), transparent);
}

.project-header h3 {
  margin: 0;
  font-size: 1.4rem;
  position: relative;
  z-index: 1;
}

.project-content {
  padding: 1.5rem;
  background-color: white;
}

.project-content p {
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.project-tags span {
  background-color: #ecf0f1;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  color: #7f8c8d;
}

.project-link {
  display: inline-block;
  color: #3498db;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s;
}

.project-link:hover {
  color: #2980b9;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  padding: 1rem;
}

.project-modal {
  background: white;
  border-radius: 8px;
  max-width: 800px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  position: relative;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: white;
  z-index: 2;
}

.modal-header {
  height: 300px;
  background-size: cover;
  background-position: center;
  position: relative;
}

.modal-header::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.7), transparent);
}

.modal-content {
  padding: 2rem;
}

.modal-content h3 {
  font-size: 1.8rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.modal-content p {
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.modal-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.modal-tags span {
  background-color: #ecf0f1;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  color: #7f8c8d;
}

.modal-link {
  display: inline-block;
  background-color: #3498db;
  color: white;
  padding: 0.8rem 1.5rem;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 600;
  transition: background-color 0.3s;
}

.modal-link:hover {
  background-color: #2980b9;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }

  .project-header {
    height: 150px;
  }

  .modal-header {
    height: 200px;
  }
}

.video-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.9);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1001; /* Higher than project modal */
}

.video-player {
  width: 80%;
  max-width: 900px;
  position: relative;
}

.video-player video {
  width: 100%;
  border-radius: 8px;
}

.video-player .close-btn {
  position: absolute;
  top: -40px;
  right: 0;
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: white;
}

.modal-link {
  display: inline-block;
  background-color: #3498db;
  color: white;
  padding: 0.8rem 1.5rem;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 600;
  transition: background-color 0.3s;
  border: none;
  cursor: pointer;
  font-family: inherit;
}

.modal-link:hover {
  background-color: #2980b9;
}

@media (max-width: 768px) {
  .video-player {
    width: 95%;
  }
}
</style>
