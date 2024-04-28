<template>
    <v-carousel
      
      style="border-radius: 12px;"
      progress="primary"
      hide-delimiters
      
    >
      <v-carousel-item
        v-for="(photo, i) in props.photos"
        :key="i"
      >
        <v-sheet
          style="height: max-content;width: max-content;border-radius: 12px;"
        >
          <div class="d-flex fill-height justify-center align-center">
            <div class="text-h2" style="background-color: #02040e;border-radius: 12px;" >   
            <v-img
                class="imgCarousel"
                :src="photo"
            >
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
            </div>
          </div>
        </v-sheet>
      </v-carousel-item>
    </v-carousel>
  </template>

<script lang="ts" setup>
import {ref,defineProps} from 'vue'

const props = defineProps({
  photos: {
    type: Array,
    required: true
  }
})


</script>
<style scoped> 

.imgCarousel{

  object-fit: scale-down;
  background-color: #02040e;
  width: 700px;
  height: 600px;
}

@media (max-width: 750px) {
.imgCarousel{
  width: 300px;
  height: 250px;
  object-fit: contain;  

}
}
</style>