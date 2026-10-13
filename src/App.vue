<script>
import HeroicComponent from './components/HeroicComponent.vue';
import NavBarComponent from './components/NavBarComponent.vue'; 
import AboutComponent from './components/AboutComponent.vue';
import SkillsComponenet from './components/SkillsComponenet.vue';
import ExperienceComponent from './components/ExperienceComponent.vue'; 
import ProjectComponent from './components/ProjectComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import ContactUsComponent from './components/ContactUsComponent.vue';
import SocialLinkComponent from './components/SocialLinkComponent.vue';
import Contact from './components/Contact.vue'

export default {
  components: {
    HeroicComponent,
    NavBarComponent,
    AboutComponent,
    SkillsComponenet,
    ExperienceComponent,
    ProjectComponent,
    FooterComponent,
    ContactUsComponent,
    SocialLinkComponent,
    Contact
  }
}
</script>


<template>
  <link rel="stylesheet" href="./css/tailwind.css" />
  
 

  <NavBarComponent />

  <HeroicComponent />

  <AboutComponent />

  <SkillsComponenet />

  <ExperienceComponent />
  
  <ProjectComponent />

  <Contact />

  <SocialLinkComponent />

  <FooterComponent />

</template>

<style scoped></style>
