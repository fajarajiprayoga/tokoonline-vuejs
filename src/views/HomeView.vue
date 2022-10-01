<template>
  <div class="home">
    
    <HeaderVue />
    <CarouselVue />
    <HomeProd />
    <InstaVue />
    <LogoPartner />
    <FooterVue />
  </div>
</template>

<script>
import HeaderVue from '@/components/HeaderVue.vue';
import CarouselVue from '@/components/CarouselVue.vue';
import HomeProd from '@/components/HomeProd.vue';
import InstaVue from '@/components/InstaVue.vue';
import LogoPartner from '@/components/LogoPartner.vue';
import FooterVue from '@/components/FooterVue.vue';


export default {
  name: 'HomeView',
  components: {
    HeaderVue,
    CarouselVue,
    HomeProd,
    InstaVue,
    LogoPartner,
    FooterVue
  }
}
</script>
