<template>
    <v-timeline align="start">
        <v-timeline-item 
            v-for="item in items" :key="item"
            :dot-color="item.color"
            fill-dot
      >
    <v-dialog
      v-model="dialog"
      width="auto"
      style="background-color: #02040e;"
    >
       <CarouselComponent :photos = "currentPhotos" />
    </v-dialog>
        <template v-slot:opposite >
            <v-card  :color ="item.color"  style="margin-bottom: 100px;">
            <v-img
               
                height="200px"
                :src= item.img[0]
                style="width:250px;border-radius:12px;cursor: pointer;"
                cover
                @click="openDialog(item.img)"
                >
                <div class="inside-picture">
                    <span >See more <v-icon icon="mdi-eye" size="x-small"></v-icon></span>
                </div>
                <template v-slot:placeholder>
                    <v-row
                        align="center"
                        class="fill-height ma-0"
                        justify="center"
                    >
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
          <v-alert class="text-h6 title"  :color="item.color">{{ item.title }}  <v-icon
                style="color: white;font-size: 20px;cursor: pointer;"
                
                icon="mdi-github"
                end
              ></v-icon></v-alert>
          <p class="description" >
             {{ item.description }}
          </p>
          <br>
          <div style="width: 100%;display: flex;flex-direction: row;flex-wrap: wrap;justify-content: start;margin-left: 10px;">
            <em v-for="(dev, index) in item.develop" :key="dev" :class="`develop text-${colors[index]}`">
                    {{ dev }}
                </em>
          </div>
          <br>
         
        </div>
    
      </v-timeline-item>
    <v-timeline-item fill-dot>
        <template v-slot:opposite>
            <h1 style="color: white;margin: auto;">And more...  <v-icon
                style="color: white;font-size: 30px;cursor: pointer;"
                
                icon="mdi-github"
                end
              ></v-icon></h1>
        </template>
      
            </v-timeline-item>
    </v-timeline>
    
  </template>







<script lang="ts" setup>
import {ref} from 'vue'
import CarouselComponent from './CarouselComponent.vue'
const colors = ["indigo","teal","red-accent-4","blue","green","deep-purple","pink"]
const dialog = ref(false);
const currentPhotos = ref([]);

function openDialog(photos) {
  currentPhotos.value = photos;
  dialog.value = true;
}
const items = [
    {
        title:"Tic Tac Toe Game",
        description:"Este juego está desarrollado el fronted y el backend, aplicando websocket para lograr una comunicacion en tiempo real y una mejor experiencia de usuario",
        develop:["Vue3","Quasar",".NetCore","Microservices","SignalR","RabbitMq","CQRS"],
        img:["/tic1.png","/tic2.png","/tic3.png","/tic4.png","/tic5.png"],
        color:"teal",
        link:"https://www.youtube.com/watch?v=HEMvsJTBweY&t=3378s",
    },
    {
        title:"Api de gestion de restaurantes",
        description:" Una api implementada para algunas de las funcionalidades de un restaurante",
        develop:["Nestjs","Microservices","Redis","RabbitMq"],
        img:["/codeApi.webp"],
        color:"indigo",
        link:"https://www.youtube.com/watch?v=HEMvsJTBweY&t=3378s"
    },
    {
        title:"Menu dinámico ",
        description:" Un proyecto para lograr la gestion completa de menú generado a traves de un Qr, implementando varias funcionalidades",
        develop:["Vue3","Quasar","Nestjs","Hexagonal Arquitecture"],
        img:["/menu11.png","/menu12.png","/menu13.png","/menu14.png",],
        color:"red-accent-4",
        link:"https://www.youtube.com/watch?v=HEMvsJTBweY&t=3378s"
    },
    {
        title:"Screen View Reescrining",
        description:"Sitio Web para empresa de restaurancion de piscinas",
        develop:["Html5","Css","Javascript"],
        img:["/pool1.png","/pool2.png","/pool3.png",],
        color:"blue",
        link:"https://www.youtube.com/watch?v=HEMvsJTBweY&t=3378s"
    },
]
</script>

<style scoped lang="scss">
.title{
    font-weight: bold;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    border-radius: 6px ;
    color: white;
    padding: 6px 20px;
}

.description{
    margin-top: 20px;
    font-size: 15px;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    margin-left: 10px;
     
}

.develop{
    font-size: 15px;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    margin-right: 10px;
    
}

.link{
    margin-top: 15px;
    color: white;
    text-decoration: none;
}
.inside-picture{
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
.inside-picture:hover{
    color: white;
    background-color: #02040e8f;
    animation: moveRigth 1.5s normal;
}
@keyframes moveRigth {
    0% { transform: translateX(-50px); }
    50% { transform: translateX(30px); }
    100% { transform: translateX(0px); }
}


</style>