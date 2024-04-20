<script setup lang="ts">
import { Ref, ref } from 'vue';
import TimelineComponent from './components/TimelineComponent.vue';
import CardProjectComponent from './components/CardProjectComponent.vue';


const experienceSection = ref(null);
const projectSection = ref(null);
const contactSection = ref(null);
const scrollToExperience = () => {
  experienceSection.value.scrollIntoView({ behavior: 'smooth' });
};
const scrollToProject = () => {
  projectSection.value.scrollIntoView({ behavior: 'smooth' });
};


const scrollToContact = () => {
  contactSection.value.scrollIntoView({ behavior: 'smooth' });
};


const firstName:Ref<string> = ref('')
const email:Ref<string> = ref('')
const phone:Ref<string> = ref("")
const content:Ref<string> = ref("");
const showSnackbar:Ref<boolean> = ref(false);
const showErrorSnackbar:Ref<boolean> = ref(false);

const submitForm = async ()=> {

      if(firstName.value!="" && email.value!=""&&content.value!="" ){
      const formData = new FormData();
      formData.append('firstName', firstName.value);
      formData.append('email', email.value);
      formData.append('phone',phone.value);
      formData.append('content',content.value);
      formData.append('_captcha', 'false');

      const response = await fetch(
        'https://formsubmit.co/miguelfernandezperez69@gmail.com',
        {
          method: 'POST',
          body: formData,
        }
      );

      if (response.ok) {
        // Aquí puedes manejar lo que sucede después de enviar el formulario.
        // Por ejemplo, puedes mostrar un mensaje de éxito.
       
        showSnackbar.value = true
      } else {
        // Aquí puedes manejar los errores.
        console.log("there was an error")
      }
    }else{
      showErrorSnackbar.value = true
    }
    }


</script>

<template>

    <v-app>      
        
        <div class="container" >
          <div class="nav-bar">
            <span @click="scrollToExperience">
                  Experience
            </span>
            <span @click="scrollToProject">
                  Projects
            </span>
  
            <span @click="scrollToContact">
                  Contact
            </span>
          </div>
          <div  class="presentation">
            <div>
              <div style="display: flex; flex-direction: row;column-gap: 40px;">
              <h1 style="font-size: 36px; font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;font-weight: bold;"> Hi, I'm Migue  </h1>
                <div class="box">Available to work</div><br>
              </div>
                <div style="margin-top: 20px;">
                <h4 style="font-size: 24px;margin-top: 20;" >+3 years of experience,
                <span style="font-size: 24px;color: rgb(209, 13, 13);font-weight: bold;"> Full Stack Developer.</span>
                Empowering ideas through innovative code.</h4>
              </div>
             
            </div>
              <div class="btn-section">
                <v-btn class="btn">
                  <a href="https://github.com/miguel807/" target="_blank" style="text-decoration: none; color: white;">
                      GitHub <v-icon
                    style="color: white;font-size: 20px;"
                    icon="mdi-github"
                    end
                    ></v-icon>
                  </a>
               </v-btn>

                <v-btn class="btn">
                  <a href="/Miguel Fernández Pérez ECV.pdf" download style="text-decoration: none;color: white;">
                      CV (en) <v-icon
                    style="color: white;font-size: 20px;"
                    icon="mdi-file-document-outline"  
                   ></v-icon>
                </a></v-btn>
                <v-btn class="btn">
                  <a href="/Miguel Fernández Pérez CV.pdf" download style="text-decoration: none;color: white;">
                  CV (es) <v-icon
                style="color: white;font-size: 20px;"
                icon="mdi-file-document-outline"
                
              ></v-icon>
            </a></v-btn>  
              </div>
          
          </div>

        
        <div ref="experienceSection" class="experienceSection " >
          
            <h2> <v-icon
             style="color: rgb(255, 0, 0);font-size: 25px;"
             icon="mdi-laptop"
      
            ></v-icon> Work Experience</h2>
                <TimelineComponent/>
            <div ref="projectSection" class="projects">
                <h2><span style="color: rgb(255, 0, 0);"> &lt;/&gt;</span> Projects</h2>
                    <CardProjectComponent  />
            </div>
           
            <div  ref="contactSection" class="contact" >

               <h2>  
                <v-icon
                style="color: rgb(255, 0, 0);font-size: 25px;"
                icon="mdi-email"
                
              ></v-icon> Contact</h2>
              
             <div class="form">
              <form  @submit.prevent="submitForm">
                <input
                class="inputForm"
                type="hidden" name="_captcha" value="false"
                 
                >
                <v-text-field
                class="inputForm"
                  v-model="firstName"
                  label="Name *"
                  variant="underlined"
                ></v-text-field>
                <v-text-field
                class="inputForm"
                  v-model="email"
                  label="Email *"
                  variant="underlined"
                ></v-text-field>
                <v-text-field
                class="inputForm"
                  v-model="phone"
                  label="Phone"
                  variant="underlined"
                  
                ></v-text-field>
                <v-textarea variant="underlined" label ="Content *" class="inputForm" rows="1"  v-model="content">

                </v-textarea>
                <v-btn class="mt-2 btn-submit"   style="background-color: transparent;"  type="submit" block >Submit  <v-icon
                icon="mdi-send"
                end
                class="icon-send"
                style="color: red;"
              ></v-icon></v-btn>
              <v-snackbar
                 v-model="showSnackbar"
                  :timeout="2000"
                  color="teal-darken-4"
                  elevation="24"
                  style="font-weight: bold;  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;"
                >
                <div class="text-center">
                <strong>Email sent successfully</strong>.
              </div>
                </v-snackbar>
                <v-snackbar
                 v-model="showErrorSnackbar"
                  :timeout="2000"
                  color="red-accent-4"
                  elevation="24"
                  style="font-weight: bold; border-radius: 20px  ;font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;"
                >
                <div class="text-center">
                <strong>All fields must be filled</strong>.
              </div>
                </v-snackbar>
         </form>
              </div>
             </div>
        </div>
        
        </div>
        
        <button class="btn-down" @click="scrollToExperience" >&UpArrow;</button>

      </v-app>

</template>

<style scoped lang="scss">
.container{
  margin: auto;
  width: 39vw;
  height: 100vh;
  min-width: 500px;
}
.nav-bar{
  margin-top:30px;
  padding-top: 10px;
  width: 100%;
  height: 50px;
  display: flex;
  justify-content: center;
  gap: 40px;
  color: white;
  font-weight: bold;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-size: small;
}
.nav-bar > span{
  text-align: center;

  width: 67px;
}
.nav-bar > span:hover{
  text-align: center;
  cursor: pointer;
  background: rgba(222, 0, 0, 0.236);
  border-radius: 12px;
  height: 19px;
  width: 67px;  
 
}


.btn-available{
  border: 1px solid white;
  font-size: 16px;
  background: transparent;
  width: 100px;
  height: 28px;
  margin-left: 14px;
  position: relative;
  top: -8px;
  padding: 4px 6px;
  border-radius: 7px;
}

.presentation{
  padding-top: 120px;
  min-width: 500px;
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: center;
  width: 80%;
  
  margin: auto;
  padding-left:45px;
}
.presentation > h1{
  color: beige;
  font-size: 44px;
  font-weight: bold;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
.presentation > h4{
  color: rgb(245, 245, 208);
  font-size: 23px;
  margin-top:13px;
  font-weight: bold;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
.btn-section{
  width: max-content;
  align-items: start;
  align-self: flex-start;
  margin-top:10px
}
.btn{
  margin: 20px 10px;
  padding: 5px 9px;
  border-radius: 16px;
  border: 2px solid rgb(26, 4, 4);
  background-color: rgb(192, 0, 0) ;
  color: white;
  width: max-content;
}
.btn:hover{
   cursor: pointer;
   background-color: rgb(255, 0, 0);
   transform: scale(1.03);
   

}

@keyframes bounce {
    0% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
    100% { transform: translateY(0); }
}


@keyframes moveRigth {
    0% { transform: translateX(0); }
    50% { transform: translateX(-8px); }
    100% { transform: translateX(0); }
}

.btn-down{
  color: rgb(236, 236, 236);
  position: absolute;
  bottom:4%;
  rotate:180deg;
  background-color: transparent;
  border: none;
  font-size: 30px;
  animation: bounce 1.5s infinite;
  left: 50%; 
  cursor: pointer;
  transform: translateX(-50%); 
  
}

@keyframes slideInFromLeft {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(0);
  }
}

.experienceElement {
  animation: 1s ease-out 0s 1 slideInFromLeft;
}

.experienceSection{
  width: 100%;
  height: max-content;
  margin-top:62%
}
.experienceSection >h2{
  margin-bottom: 60px;
  color: white;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  margin-top:20px;
  font-weight: bold;
  font-size: 25px;
}
.projects{
  margin-top:100px ;
  width: 100%;
  height: max-content;
}
.projects>h2{
  color: white;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  margin-top:20px;
  font-weight: bold;
  font-size: 25px;
  margin-bottom: 20px;
}

.contact{
  margin-top: 70px;
  color: white;
  font-size: 20px;
  width: 100%;
  height: max-content;
  padding-bottom: 50px;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;

}

.form{
  margin: auto;
  margin-top: 30px;
  width: 80%;
  border: 1px solid rgba(255, 255, 255, 0.16);
  box-shadow: 1px 1px 1px 1px rgba(102, 100, 100, 0.164);
  padding: 20px;
  border-radius: 18px;
 
}
.inputForm{
  border-radius: 25px;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  padding-left: 10px;
  background: transparent;
}
.btn-submit{
  border-radius: 16px;
  width: max-content;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: bold;
  
  
}
.icon-send{
  animation:  moveRigth 1.7s infinite;
  margin-left: 10px;
  
}




.box {
  cursor: pointer;
  width: 150px;
  height: 30px;
  display: grid;
  place-content: center;
  color: white;
  text-shadow: 0 1px 0 #000;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-size: small;
  --border-angle: 0turn; // For animation.
  --main-bg: conic-gradient(
      from var(--border-angle),
      #213,
      #112 5%,
      #112 60%,
      #213 95%
    );
  
  border: solid 3px transparent;
  border-radius: 2em;
  --gradient-border: conic-gradient(from var(--border-angle), transparent 25%, #08f, rgb(255, 0, 0) 99%, transparent);
  
  background: 
    // padding-box clip this background in to the overall element except the border.
    var(--main-bg) padding-box,
    // border-box extends this background to the border space
    var(--gradient-border) border-box, 
    // Duplicate main background to fill in behind the gradient border. You can remove this if you want the border to extend "outside" the box background.
    var(--main-bg) border-box;
  
  background-position: center center;

  animation: bg-spin 3s linear infinite;
  @keyframes bg-spin {
    to {
      --border-angle: 1turn;
    }
  }

  &:hover {
    animation-play-state: paused;
  }
}

@property --border-angle {
  syntax: "<angle>";
  inherits: true;
  initial-value: 0turn;
}
</style>
