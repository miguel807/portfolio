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
            <div class="text-h2" style="background-color: #02040e;border-radius: 12px;">   
            <v-img
                style="width: 500px;height: 400px;object-fit: scale-down;background-color: #02040e;"
                
                :src="photo"
            ></v-img>
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
console.log(props.photos)

</script>
<style scoped> 
</style>