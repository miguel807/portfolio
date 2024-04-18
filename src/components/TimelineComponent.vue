<template>
    <v-timeline side="end" >
      <v-timeline-item
        v-for="item in items"
        :key="item.id"
        :dot-color="item.color"
        fill-dot
        size="small"
        
        
      >
        <v-alert
          :color="item.background"
          style="border-radius: 9px;"
          :value="true"
        >
          <div>
            <span style="color: red;margin-right: 10px;">{{ item.date }}</span>
            <span style="font-size: 12px;">{{ item.title }}</span> <br><br>
            <h3 style="font-size: 15px;font-weight: lighter;">{{ item.description }}</h3>
          </div>
        </v-alert>
      </v-timeline-item >
    </v-timeline>
  </template>
<script lang="ts" setup>
const items =  [
        {
          id: 1,
          color: 'red-accent-4',
          background:"#030008",
          icon: '',
          date:"2022-present",
          title: "Full Stack Engineer - Geocuba ",
          description:"As a Full Stack Developer, I led projects encompassing both frontend and backend development, implementing innovative solutions that enhanced user experience and boosted system efficiency. I contributed to the design and implementation of new features, ensuring seamless integration between frontend and backend components. Some of these projects included the disaster management system (Fenix) and the management system for workers of a specific company."
        },
        {
          id: 2,
          color: 'red-accent-4',
          background:"#030008",
          icon: '',
          date: "2021-2022",
          title:"Frontend Engineer ",
          description:
"As a frontend developer, I played a pivotal role in crafting a dynamic website for a pool repair company. Leveraging modern web technologies, I designed and implemented intuitive user interfaces that showcased the company's services and expertise effectively. Through meticulous attention to detail and responsive design principles, I ensured the website provided a seamless and engaging experience for visitors across various devices. Additionally, I collaborated closely with designers and backend developers to integrate backend functionalities seamlessly, enabling features such as appointment scheduling and service inquiries to enhance customer interaction and satisfaction."
        },
        
      ]
    
</script>
<style scoped>
.dot:hover{
  transform: scale(1.2);

}
.dot{
  cursor: pointer;
}
</style>