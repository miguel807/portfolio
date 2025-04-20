<template>
  <v-timeline align="start" class="show-on-small">
    <v-timeline-item
      v-for="item in items"
      :key="item"
      :dot-color="item.color"
      fill-dot
    >
      <v-dialog v-model="dialog" width="auto" style="background-color: #02040e">
        <CarouselComponent :photos="currentPhotos" />
      </v-dialog>
      <template v-slot:opposite>
        <v-card :color="item.color" style="margin-bottom: 100px">
          <v-img
            height="200px"
            :src="item.img[0]"
            style="width: 300px; border-radius: 12px; cursor: pointer"
            cover
            @click="openDialog(item.img)"
          >
            <div class="inside-picture">
              <span
                >See more <v-icon icon="mdi-eye" size="x-small"></v-icon
              ></span>
            </div>
            <template v-slot:placeholder>
              <v-row align="center" class="fill-height ma-0" justify="center">
                <v-progress-circular
                  color="grey-lighten-5"
                  indeterminate
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-card>
      </template>
      <div>
        <v-alert class="text-h6 title" :color="item.color"
          >{{ item.title }}
          <a
            v-bind:href="item.link"
            target="_blank"
            style="text-decoration: none"
          >
            <v-icon
              style="color: white; font-size: 20px; cursor: pointer"
              icon="mdi-github"
              end
            ></v-icon></a
        ></v-alert>
        <p class="description">
          {{ item.description }}
        </p>
        <br />
        <div
          style="
            width: 100%;
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: start;
            margin-left: 10px;
          "
        >
          <em
            v-for="(dev, index) in item.develop"
            :key="dev"
            :class="`develop text-${colors[index]}`"
          >
            {{ dev }}
          </em>
        </div>
        <br />
      </div>
    </v-timeline-item>
    <v-timeline-item fill-dot>
      <template v-slot:opposite>
        <h1 style="color: white; margin: auto">
          And more...
          <a
            href="https://github.com/miguel807/"
            target="_blank"
            style="text-decoration: none"
          >
            <v-icon
              style="color: white; font-size: 30px; cursor: pointer"
              icon="mdi-github"
              end
            ></v-icon>
          </a>
        </h1>
      </template>
    </v-timeline-item>
  </v-timeline>

  <!--esto es en el responsive-->

  <v-timeline side="end" class="hide-on-small" style="margin-right: 20px">
    <v-timeline-item
      v-for="item in items"
      :key="item"
      :dot-color="item.color"
      fill-dot
      size="small"
    >
      <v-alert color="transparent" style="border-radius: 9px" :value="true">
        <div>
          <v-card
            :style="{
              'margin-bottom': '20px',
              'background-color': 'transparent',
              border: `1px solid ${item.colorHex}`,
              'border-radius': '9px',
            }"
          >
            <v-alert
              class="title"
              :color="item.color"
              style="
                border-radius: 9px 9px 0px 0px;
                font-size: 25px;
                font-family: 'Gill Sans', 'Gill Sans MT', Calibri,
                  'Trebuchet MS', sans-serif;
              "
              >{{ item.title }}
              <a
                v-bind:href="item.link"
                target="_blank"
                style="text-decoration: none"
              >
                <v-icon
                  style="color: white; font-size: 25px; cursor: pointer"
                  icon="mdi-github"
                  end
                ></v-icon></a
            ></v-alert>
            <v-img
              height="250px"
              :src="item.img[0]"
              style="
                width: 100%;
                border-radius: 0px;
                cursor: pointer;
                background-color: transparent;
              "
              cover
              @click="openDialog(item.img)"
            >
              <div class="inside-picture">
                <span
                  >See more <v-icon icon="mdi-eye" size="x-small"></v-icon
                ></span>
              </div>
              <template v-slot:placeholder>
                <v-row align="center" class="fill-height ma-0" justify="center">
                  <v-progress-circular
                    color="grey-lighten-5"
                    indeterminate
                  ></v-progress-circular>
                </v-row>
              </template>
            </v-img>
            <div>
              <h3
                class="description"
                style="
                  margin-top: 20px;
                  margin-left: 15px;
                  margin-right: 15px;
                  font-size: 23px;
                  text-align: center;
                "
              >
                {{ item.description }}
              </h3>
              <br />

              <div
                style="
                  width: 100%;
                  
                  display: flex;
                  flex-direction: row;
                  flex-wrap: wrap;
                  justify-content: center;
                  margin-left: 10px;
                  padding: 5px;
                  column-gap: 12px;
                  row-gap: 4px;
                  
                "
              >
                <em
                  v-for="(dev, index) in item.develop"
                  :key="dev"
                  :class="`develop text-${colors[index]}`"
                  style="font-size: 14px"
                >
                  {{ dev }}
                </em>
              </div>

              <br />
            </div>
          </v-card>
        </div>
      </v-alert>
    </v-timeline-item>
  </v-timeline>
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
.title {
  font-weight: bold;

  border-radius: 6px;
  color: white;
  padding: 6px 20px;
}

.description {
  margin-top: 20px;
  margin-left: 10px;
  margin-right: 10px;
  font-size: 15px;
  color: #cfd8dc;
  font-weight: 300;
  line-height: 1.5;
}

.develop {
  font-size: 14px;
  margin-right: 10px;
}

.link {
  margin-top: 15px;
  color: white;
  text-decoration: none;
}
.inside-picture {
  width: 100%;
  height: 100%;
  background: transparent;
  font-size: 20px;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: center;
  color: transparent;
}
.inside-picture:hover {
  color: white;
  background-color: #02040e8f;
  animation: moveRigth 1s normal;
}
@keyframes moveRigth {
  0% {
    transform: translateY(-5px);
  }
  50% {
    transform: translateY(5px);
  }
  100% {
    transform: translateY(0px);
  }
}

/* styles.css */
@media (min-width: 750px) {
  .hide-on-small {
    display: none;
  }
}
@media (max-width: 750px) {
  .show-on-small {
    display: none;
  }
}
</style>