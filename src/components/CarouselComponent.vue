<template>
  <v-carousel
    style="border-radius: 12px;"
    progress="red"
    hide-delimiters
    height="70vh"
  >
    <v-carousel-item
      v-for="(photo, i) in props.photos"
      :key="i"
    >
      <div class="d-flex fill-height justify-center align-center carousel-item-container">
        <v-img
          :src="photo"
          class="imgCarousel"
          max-height="100%"
          max-width="100%"
          contain
        >
          <template v-slot:placeholder>
            <v-row align="center" class="fill-height ma-0" justify="center">
              <v-progress-circular
                color="red"
                indeterminate
              ></v-progress-circular>
            </v-row>
          </template>
        </v-img>
      </div>
    </v-carousel-item>
  </v-carousel>
</template>

<script lang="ts" setup>
import { defineProps } from 'vue'

const props = defineProps({
  photos: {
    type: Array,
    required: true
  }
})
</script>

<style scoped>
.carousel-item-container {
  background-color: transparent;
  padding: 0;
}

.imgCarousel {
  border-radius: 8px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}
</style>