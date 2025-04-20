<template>
  <v-timeline side="end" class="work">
    <v-timeline-item
      v-for="item in items"
      :key="item.id"
      :dot-color="item.color"
      fill-dot
      size="small"
    >
      <v-alert
        :color="item.background"
        style="
          border-radius: 12px;
          background: linear-gradient(145deg, #121212, #1e1e2f);
          box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.6);
        "
        :value="true"
      >
        <div class="section">
          <span class="section-date">{{ item.date }}</span>
          <span class="section-title">{{ item.title }}</span> <br /><br />
          <h3 class="section-description">{{ item.description }}</h3>
          <br />
          <div
            style="
              width: 100%;
              display: flex;
              flex-direction: row;
              flex-wrap: wrap;
              justify-content: center;
              margin-left: 10px;
              padding-left: 15px;
              padding-right: 15px;
              column-gap: 12px;
              row-gap: 4px;
            "
          >
            <em
              v-for="(data, index) in item.develop"
              :key="index"
              :class="`develop text-${colors[index]}`"
              style="font-size: 14px"
            >
              {{ data }}
            </em>
          </div>
        </div>
      </v-alert>
    </v-timeline-item>
  </v-timeline>
</template>
<script lang="ts" setup>
const colors = [
  "indigo",
  "teal",
  "red-accent-4",
  "blue",
  "green",
  "deep-purple",
  "pink",
  "indigo",
  "teal",
  "red-accent-4",
];
const items = [
  {
    id: 1,
    color: "red-accent-4",
    background: "#121212",
    icon: "",
    date: "02/2022 - 01/2025",
    title: "Full Stack Developer - Geocuba ",
    description:
      "I developed and implemented end-to-end solutions covering both frontend and backend. I implemented automated tests that improved the system's reliability and scalability, and resolved critical issues, reducing response times and enhancing user experience. Notable projects include the disaster management system (Fénix) and a platform for company personnel administration.",
    develop: [
      ".Net Core",
      "SqlServer",
      "Entity Framework",
      "SignalR",
      "React",
      "Tailwind",
    ],
  },
  {
    id: 2,
    color: "red-accent-4",
    background: "#121212",
    icon: "",
    date: "03/2023 - 07/2023",
    title: "Backend Developer - Informage Studios",
    description:
      "As a backend developer, I participated in the implementation and update of application modules under the guidance of a senior team. I was responsible for identifying and resolving critical issues, improving the overall quality of the system, and supporting the integration of new features through effective communication with all involved parties.",
    develop: [
      "NestJs",
      "Docker",
      "MongoDB",
      "Socket.io",
      "Hexagonal Arquitecture",
    ],
  },
  {
    id: 3,
    color: "red-accent-4",
    background: "#121212",
    icon: "",
    date: "01/2024 - 11/2024",
    title: "Full Stack Developer - Tecopos ",
    description:
      " As a Full Stack developer, I was responsible for developing scalable and modular solutions based on microservices. I actively participated in requirements analysis with the client and clearly documented the developed functionalities to facilitate their maintenance and scalability. Additionally, I collaborated closely with various teams to ensure successful system integration.",
    develop: [
      "NestJS",
      "PostgreSql",
      "Prisma",
      "Docker",
      "Nats",
      "Kafka",
      "Socket.io",
      "React",
      "Tailwind",
      "Redux",
    ],
  },
];
</script>
<style scoped>
.dot:hover {
  transform: scale(1.2);
}
.dot {
  cursor: pointer;
}
.section-title {
  font-size: 16px;
  font-weight: 600;
  color: #ffffff;
}
.section-date {
  font-size: 13px;
  margin-right: 9px;
  color: #e53935; /* un rojo más suave y profesional */
}
.section {
  padding: 16px;
}
.section-description {
  font-size: 15px;
  color: #cfd8dc;
  font-weight: 300;

  line-height: 1.5;
}

@media (max-width: 750px) {
  .work {
    margin-right: 20px;
  }
  .section {
    padding: 16px;
  }
  .section-title {
    font-size: 16px;
    font-weight: 600;
    color: #ffffff;
  }
  .section-date {
    font-size: 13px;
    margin-right: 9px;
    color: #e53935; /* un rojo más suave y profesional */
  }
  .section-description {
    font-size: 15px;
    color: #cfd8dc;
    font-weight: 300;
    line-height: 1.5;
  }
}

.background-color-indigo {
  background-color: indigo;
}

.background-color-teal {
  background-color: teal;
}

.background-color-red-accent-4 {
  background-color: #d32f2f; /* Puedes ajustar el valor hex si es necesario */
}

.background-color-blue {
  background-color: blue;
}

.background-color-green {
  background-color: green;
}

.background-color-deep-purple {
  background-color: #673ab7;
}

.background-color-pink {
  background-color: pink;
}
</style>