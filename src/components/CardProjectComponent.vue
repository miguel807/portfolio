<template>
  <div class="projects-grid">
    <v-row>
      <v-col
        v-for="(item, index) in items"
        :key="index"
        cols="12"
        md="6"
        class="project-col"
      >
        <v-card class="project-card" :style="{ '--accent-color': item.colorHex }">
          <div class="card-image-container" @click="openDialog(item.img)">
            <v-img
              :src="item.img[0]"
              height="240"
              cover
              class="project-image"
            >
              <div class="image-overlay">
                <v-icon icon="mdi-eye" color="white" size="large"></v-icon>
                <span>View Details</span>
              </div>
            </v-img>
          </div>

          <div class="card-content">
            <div class="card-header">
              <h3 class="project-title">{{ item.title }}</h3>
              <a
                v-if="item.link"
                :href="item.link"
                target="_blank"
                class="github-link"
              >
                <v-icon icon="mdi-github" size="large"></v-icon>
              </a>
            </div>

            <p class="project-description">{{ item.description }}</p>

            <div class="tech-stack">
              <span
                v-for="(tech, tIndex) in item.develop"
                :key="tIndex"
                class="tech-tag"
                :style="{ color: item.colorHex }"
              >
                {{ tech }}
              </span>
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>

    <v-dialog v-model="dialog" max-width="900" class="project-dialog">
      <v-card color="transparent" elevation="0">
        <CarouselComponent :photos="currentPhotos" />
      </v-card>
    </v-dialog>

    <div class="more-projects">
      <p>Want to see more?</p>
      <a href="https://github.com/miguel807/" target="_blank" class="github-cta">
        Check my GitHub <v-icon icon="mdi-github" end></v-icon>
      </a>
    </div>
  </div>
</template>







<script lang="ts" setup>
import { ref } from "vue";
import CarouselComponent from "./CarouselComponent.vue";
const colors = [
  "indigo",
  "teal",
  "red-accent-4",
  "blue",
  "green",
  "deep-purple",
  "pink",
];
const dialog = ref(false);
const currentPhotos = ref([]);

function openDialog(photos) {
  currentPhotos.value = photos;
  dialog.value = true;
}
const items = [
  {
    title: "Tic Tac Toe Game",
    description:
      "This game is developed with both frontend and backend, applying websocket to achieve real-time communication and a better user experience.",
    develop: [
      "Vue3",
      "Quasar",
      ".NetCore",
      "Microservices",
      "SignalR",
      "RabbitMq",
      "CQRS",
    ],
    img: ["/tic1.png", "/tic2.png", "/tic3.png", "/tic4.png", "/tic5.png"],
    color: "teal",
    link: "https://github.com/miguel807/ticTacToeApi",
    colorHex: "#009688",
  },
  {
    title: "Restaurant Management API",
    description:
      "An API implemented for some of the functionalities of a restaurant.",
    develop: ["Nestjs", "Microservices", "Redis", "RabbitMq"],
    img: ["/codeApi.webp"],
    color: "indigo",
    link: "",
    colorHex: "#3F51B5",
  },
  {
    title: "Dynamic Menu",
    description:
      "A project to achieve complete management of a menu generated through a QR code, implementing its functionalities.",
    develop: ["Vue3", "Quasar", "Nestjs", "Hexagonal Arquitecture"],
    img: ["/menu11.png", "/menu12.png", "/menu13.png", "/menu14.png"],
    color: "red-accent-4",
    link: "https://github.com/miguel807/Alinas/tree/master",
    colorHex: "#D50000",
  },
  {
    title: "Screen View Rescreening",
    description:
      "Website for a company responsible for maintenance and repair tasks.",
    develop: ["Html5", "Css", "Javascript"],
    img: ["/pool1.png", "/pool2.png", "/pool3.png"],
    color: "blue",
    link: "https://github.com/miguel807/clearViewRes",
    colorHex: "#2196F3",
  },
];
</script>

<style scoped lang="scss">
.projects-grid {
  width: 100%;
  padding: 20px 0;
}

.project-card {
  background: rgba(255, 255, 255, 0.03) !important;
  backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.08) !important;
  border-radius: 20px !important;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
  height: 100%;
  display: flex;
  flex-direction: column;

  &:hover {
    transform: translateY(-8px);
    border-color: var(--accent-color) !important;
    background: rgba(255, 255, 255, 0.05) !important;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4), 0 0 20px rgba(var(--accent-color), 0.1);

    .project-image {
      transform: scale(1.05);
    }

    .image-overlay {
      opacity: 1;
    }
  }
}

.card-image-container {
  overflow: hidden;
  position: relative;
  cursor: pointer;
}

.project-image {
  transition: transform 0.6s ease;
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
  gap: 10px;

  span {
    color: white;
    font-weight: 600;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 1px;
  }
}

.card-content {
  padding: 24px;
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 12px;
}

.project-title {
  font-size: 22px;
  font-weight: 700;
  color: #fff;
  line-height: 1.2;
}

.github-link {
  color: rgba(255, 255, 255, 0.6);
  transition: color 0.3s ease;

  &:hover {
    color: #fff;
  }
}

.project-description {
  font-size: 15px;
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.6;
  margin-bottom: 20px;
  font-weight: 300;
}

.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: auto;
}

.tech-tag {
  font-size: 12px;
  font-weight: 600;
  padding: 4px 10px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 100px;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

.more-projects {
  margin-top: 60px;
  text-align: center;
  padding: 40px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);

  p {
    color: rgba(255, 255, 255, 0.5);
    margin-bottom: 10px;
  }
}

.github-cta {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-size: 20px;
  font-weight: 700;
  color: #fff;
  text-decoration: none;
  transition: transform 0.3s ease;

  &:hover {
    transform: scale(1.05);
    color: #ff3c3c;
  }
}

@media (max-width: 600px) {
  .project-col {
    padding: 12px !important;
  }
  
  .project-title {
    font-size: 18px;
  }
}
</style>