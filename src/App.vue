<script setup lang="ts">
import { onMounted, Ref, ref } from "vue";
import TimelineComponent from "./components/TimelineComponent.vue";
import CardProjectComponent from "./components/CardProjectComponent.vue";

const experienceSection = ref(null);
const projectSection = ref(null);
const contactSection = ref(null);
const heightScreen = ref(0);
const loading = ref(true);
onMounted(() => {
  setTimeout(() => {
    loading.value = false;
  }, 2000);
  heightScreen.value = window.innerHeight;
  console.log(heightScreen.value);
});
const scrollToExperience = () => {
  experienceSection.value.scrollIntoView({ behavior: "smooth" });
};
const scrollToProject = () => {
  projectSection.value.scrollIntoView({ behavior: "smooth" });
};

const scrollToContact = () => {
  contactSection.value.scrollIntoView({ behavior: "smooth" });
};

const firstName: Ref<string> = ref("");
const email: Ref<string> = ref("");
const phone: Ref<string> = ref("");
const content: Ref<string> = ref("");
const showSnackbar: Ref<boolean> = ref(false);
const showErrorSnackbar: Ref<boolean> = ref(false);
const isLoadingForm: Ref<boolean> = ref(false);

const submitForm = async () => {
  isLoadingForm.value = true;
  if (firstName.value != "" && email.value != "" && content.value != "") {
    const formData = new FormData();
    formData.append("firstName", firstName.value);
    formData.append("email", email.value);
    formData.append("phone", phone.value);
    formData.append("content", content.value);
    formData.append("_captcha", "false");

    const response = await fetch(
      "https://formsubmit.co/miguelfernandezperez69@gmail.com",
      {
        method: "POST",
        body: formData,
      }
    );

    if (response.ok) {
      email.value = "";
      firstName.value = "";
      phone.value = "";
      content.value = "";

      showSnackbar.value = true;
      isLoadingForm.value = false;
    } else {
      // Aquí puedes manejar los errores.
      console.log("there was an error");
      isLoadingForm.value = false;
    }
  } else {
    showErrorSnackbar.value = true;
    isLoadingForm.value = false;
  }
};
</script>

<template>
  <v-app>
    <div v-if="loading" class="loading-spinner">
      <v-progress-circular
        indeterminate
        color="red"
        size="64"
        width="7"
      ></v-progress-circular>
    </div>
    <div v-else>
      <div class="container">
        <div class="nav-bar">
          <span @click="scrollToExperience"> Experience </span>
          <span @click="scrollToProject"> Projects </span>

          <span @click="scrollToContact"> Contact </span>
        </div>
        <div class="presentation">
          <div class="hero-content">
            <div class="hero-top">
              <h1 class="hero-name">Hi, I'm Migue</h1>
              <div class="box">Available to work</div>
            </div>
            <div class="hero-summary">
              <h4 class="hero-description">
                +3 years of experience,
                <span class="hero-highlight">
                  Full Stack Developer.</span>
                Empowering ideas through innovative code.
              </h4>
            </div>
          </div>
          <div class="btn-section">
            <v-btn class="btn">
              <a
                href="https://github.com/miguel807/"
                target="_blank"
                style="text-decoration: none; color: white"
              >
                GitHub
                <v-icon
                  style="color: white; font-size: 20px"
                  icon="mdi-github"
                  end
                ></v-icon>
              </a>
            </v-btn>

            <v-btn class="btn">
              <a
                href="/CV_Miguel_Fernandez_Software_Engineer_EN.pdf"
                download
                style="text-decoration: none; color: white"
              >
                CV (en)
                <v-icon
                  style="color: white; font-size: 20px"
                  icon="mdi-file-document-outline"
                ></v-icon> </a
            ></v-btn>
            <v-btn class="btn">
              <a
                href="/CV_Miguel_Fernandez_Software_Engineer_ES.pdf"
                download
                style="text-decoration: none; color: white"
              >
                CV (es)
                <v-icon
                  style="color: white; font-size: 20px"
                  icon="mdi-file-document-outline"
                ></v-icon> </a
            ></v-btn>
          </div>
          <div class="scroll-arrow" @click="scrollToExperience">
            <v-icon icon="mdi-chevron-down" size="x-large"></v-icon>
          </div>
        </div>

        <div ref="experienceSection" class="experienceSection">
          <h2 class="workExperienceMovile">
            <v-icon
              style="color: rgb(255, 0, 0); font-size: 25px"
              icon="mdi-laptop"
            ></v-icon>
            Work Experience
          </h2>
          <TimelineComponent />
          <div ref="projectSection" class="projects">
            <h2 class="projectSectionMovile">
              <span style="color: rgb(255, 0, 0)"> &lt;/&gt;</span> Projects
            </h2>
            <CardProjectComponent />
          </div>

          <div ref="contactSection" class="contact">
            <h2>
              <v-icon
                style="color: rgb(255, 0, 0); font-size: 25px"
                icon="mdi-email"
              ></v-icon>
              Contact
            </h2>

            <div class="form">
              <form @submit.prevent="submitForm">
                <input
                  class="inputForm"
                  type="hidden"
                  name="_captcha"
                  value="false"
                />
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
                <v-textarea
                  variant="underlined"
                  label="Content *"
                  class="inputForm"
                  rows="1"
                  v-model="content"
                >
                </v-textarea>
                <v-btn
                  class="mt-2 btn-submit"
                  :disabled="isLoadingForm"
                  style="background-color: transparent"
                  type="submit"
                  block
                  >Submit
                  <v-icon
                    icon="mdi-send"
                    end
                    class= "icon-send"
                    :style= "!isLoadingForm ? 'color: red;':'display:none;'"
                    
                  ></v-icon
                ></v-btn>
                <v-snackbar
                  v-model="showSnackbar"
                  :timeout="2000"
                  color="teal-darken-4"
                  elevation="24"
                  style="font-weight: bold"
                >
                  <div class="text-center">
                    <span>Email sent successfully</span>.
                  </div>
                </v-snackbar>
                <v-snackbar
                  v-model="showErrorSnackbar"
                  :timeout="2000"
                  color="red-accent-4"
                  elevation="24"
                  style="font-weight: bold; border-radius: 20px"
                >
                  <div class="text-center">
                    <span>All fields must be filled</span>.
                  </div>
                </v-snackbar>
              </form>
            </div>
          </div>
        </div>
      </div>

    </div>
  </v-app>
</template>

<style scoped lang="scss">
.container {
  margin: auto;
  width: 90%;
  max-width: 1000px;
  min-height: 100vh;
}
.nav-bar {
  margin-top: 30px;
  padding-top: 10px;
  width: 100%;
  height: 50px;
  display: flex;
  justify-content: center;
  gap: 40px;
  color: white;
  font-weight: bold;
  font-size: small;
}
.loading-spinner {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1000; /* Asegúrate de que el spinner esté sobre otros elementos */
}
.nav-bar > span {
  text-align: center;

  width: 67px;
}
.nav-bar > span:hover {
  text-align: center;
  cursor: pointer;
  background: rgba(222, 0, 0, 0.236);
  border-radius: 12px;
  height: 19px;
  width: 67px;
}

.btn-available {
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

.presentation {
  padding-top: 15vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  min-height: 85vh;
  position: relative;
}

.hero-top {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  column-gap: 20px;
  margin-bottom: 20px;
}

.hero-name {
  font-size: clamp(36px, 5vw, 56px) !important;
  font-weight: bold;
  color: #fff;
  line-height: 1.1;
}

.hero-highlight {
  color: #ff3c3c;
  font-weight: 800;
  background: linear-gradient(90deg, #ff3c3c, #ff8a8a);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-description {
  color: rgba(255, 255, 255, 0.8);
  font-size: clamp(20px, 3vw, 24px) !important;
  line-height: 1.4;
  font-weight: 400;
}
.btn-section {
  width: max-content;
  display: flex;
  align-items: center;
  align-self: center;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 10px;
}
.btn {
  margin: 20px 10px;
  padding: 5px 9px;
  border-radius: 16px;
  border: 2px solid rgb(26, 4, 4);
  background-color: rgb(192, 0, 0);
  color: white;
  width: max-content;
}
.btn:hover {
  cursor: pointer;
  background-color: rgb(255, 0, 0);
  transform: scale(1.03);
}

.scroll-arrow {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  color: rgba(255, 255, 255, 0.6);
  cursor: pointer;
  animation: bounce 2s infinite;
  transition: color 0.3s ease;

  &:hover {
    color: #ff3c3c;
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateX(-50%) translateY(0);
  }
  40% {
    transform: translateX(-50%) translateY(-10px);
  }
  60% {
    transform: translateX(-50%) translateY(-5px);
  }
}

.experienceElement {
  animation: 1s ease-out 0s 1 slideInFromLeft;
}

.experienceElement {
  animation: 1s ease-out 0s 1 slideInFromLeft;
}

.experienceSection {
  width: 100%;
  height: max-content;
  margin-top: 70%;
}
.experienceSection > h2 {
  margin-bottom: 60px;
  color: white;

  margin-top: 20px;
  font-weight: bold;
  font-size: 25px;
}
.projects {
  margin-top: 100px;
  width: 100%;
  height: max-content;
}
.projects > h2 {
  color: white;

  margin-top: 20px;
  font-weight: bold;
  font-size: 25px;
  margin-bottom: 20px;
}

.contact {
  margin-top: 70px;
  color: white;
  font-size: 20px;
  width: 100%;
  height: max-content;
  padding-bottom: 50px;
}

.form {
  margin: auto;
  margin-top: 30px;
  width: 80%;
  border: 1px solid rgba(255, 255, 255, 0.16);
  box-shadow: 1px 1px 1px 1px rgba(102, 100, 100, 0.164);
  padding: 20px;
  border-radius: 18px;
}
.inputForm {
  border-radius: 25px;

  padding-left: 10px;
  background: transparent;
}
.btn-submit {
  border-radius: 16px;
  width: max-content;

  font-weight: bold;
}
.icon-send {
  animation: moveRigth 1.7s infinite;
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
  --gradient-border: conic-gradient(
    from var(--border-angle),
    transparent 25%,
    #08f,
    rgb(255, 0, 0) 99%,
    transparent
  );

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

@media (max-width: 750px) {
  .contact > h2 {
    margin-left: 20px;
  }
  .workExperienceMovile {
    margin-left: 22px;
    font-size: 35px;
  }
  .projectSectionMovile {
    margin-left: 20px;
    font-size: 35px;
  }
  .form {
    width: 84%;
  }
  .presentation {
    padding-right: 20px;
    position: relative;

    height: 100vh;
    top: -120px;
  }
  .container {
    height: 100vh;
  }
}
</style>
