<template>
  <v-timeline side="end" class="experience-timeline">
    <v-timeline-item
      v-for="item in items"
      :key="item.id"
      dot-color="#ff3c3c"
      fill-dot
      size="small"
    >
      <v-card class="experience-card">
        <div class="experience-content">
          <div class="experience-header">
            <span class="experience-date">{{ item.date }}</span>
            <h3 class="experience-title">{{ item.title }}</h3>
          </div>
          
          <p class="experience-description">{{ item.description }}</p>

          <div class="experience-tech">
            <span
              v-for="(tech, index) in item.develop"
              :key="index"
              class="tech-tag"
            >
              {{ tech }}
            </span>
          </div>
        </div>
      </v-card>
    </v-timeline-item>
  </v-timeline>
</template>

<script lang="ts" setup>
const items = [
  {
    id: 1,
    color: "red-accent-4",
    date: "05/2025 – Present",
    title: "Fullstack Developer - Bicimex",
    description:
      "Internal Systems Architecture: Design and development of custom Add-ons for warehouse management, optimizing fulfillment speed and inventory movement. Process Automation: Implementation of purchasing automation flows using n8n, reducing manual errors. Microservices and Cloud: Development of high-performance microservices and APIs using Django and FastAPI on Google Cloud Platform.",
    develop: [
      "Django",
      "FastAPI",
      "n8n",
      "GCP",
      "Python",
      "Vue.js",
    ],
  },
  {
    id: 2,
    color: "red-accent-4",
    date: "02/2024 – 03/2025",
    title: "FullStack Developer - Tecopos",
    description:
      "Distributed Systems: Designed microservices-based solutions using NestJS, Kafka, and Nats, ensuring robust asynchronous communication between modules. Initial Technical Leadership: Conducted critical requirements analysis directly with clients and generated structural technical documentation for engineering teams.",
    develop: [
      "NestJS",
      "PostgreSQL",
      "Kafka",
      "Nats",
      "Docker",
      "Microservices",
    ],
  },
  {
    id: 3,
    color: "red-accent-4",
    date: "03/2022 – 09/2023",
    title: "Backend Developer - Informage Studios",
    description:
      "Backend Service Development: Participated in the construction and maintenance of services using .NET Core and SQL Server, ensuring data integrity through Entity Framework. Real-time Interactivity: Implemented SignalR for bidirectional communication. System Robustness: Collaborated on automated testing and incident diagnosis in production, optimizing stability.",
    develop: [
      ".Net Core",
      "SqlServer",
      "Entity Framework",
      "SignalR",
      "Unit Testing",
    ],
  },
];
</script>

<style scoped lang="scss">
.experience-timeline {
  margin-top: 40px;
}

.experience-card {
  background: rgba(255, 255, 255, 0.03) !important;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.08) !important;
  border-radius: 16px !important;
  transition: all 0.3s ease;
  margin-bottom: 24px;

  &:hover {
    background: rgba(255, 255, 255, 0.05) !important;
    border-color: rgba(255, 60, 60, 0.3) !important;
    transform: translateX(5px);
  }
}

.experience-content {
  padding: 24px;
}

.experience-header {
  margin-bottom: 12px;
}

.experience-date {
  display: block;
  font-size: 13px;
  font-weight: 600;
  color: #ff3c3c;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 4px;
}

.experience-title {
  font-size: 18px;
  font-weight: 700;
  color: #fff;
}

.experience-description {
  font-size: 15px;
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.6;
  font-weight: 300;
  margin-bottom: 20px;
}

.experience-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tech-tag {
  font-size: 11px;
  font-weight: 600;
  padding: 3px 10px;
  background: rgba(255, 255, 255, 0.05);
  color: rgba(255, 255, 255, 0.8);
  border-radius: 100px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

@media (max-width: 600px) {
  .experience-content {
    padding: 16px;
  }
  
  .experience-title {
    font-size: 16px;
  }
}
</style>