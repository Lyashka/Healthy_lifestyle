<template>
  <v-app>
    <v-app-bar>  
    <v-app-bar-title>Healthy Lifestyle</v-app-bar-title>
   
    <template #append>
      <RouterLink 
        class="closeStyle" to="/">
        <v-btn 
          v-if="!isNarrowScreen"
          text="Главная"
        />
        <v-btn 
          v-else 
          icon="mdi-home" 
          size="x-large"
        />
      </RouterLink>
      <RouterLink class="closeStyle" to="/Statistics">
        <v-btn 
          v-if="!isNarrowScreen"
          text="Статистика"
        />
        <v-btn 
          v-else 
          icon="mdi-chart-bar" 
          size="x-large"
        />
      </RouterLink>
      <RouterLink class="closeStyle" to="/Guide">
        <v-btn 
          v-if="!isNarrowScreen"
          text="Справочник"
        />
        <v-btn 
          v-else 
          icon="mdi-book-search" 
          size="x-large"
        />
      </RouterLink>
    </template>
  </v-app-bar>
  
  <v-main>
    <Personalization v-if="statusMenu"/>
    <RouterView />
  </v-main>
  
  </v-app>  
  </template>

<script setup> 
import { RouterView, RouterLink } from 'vue-router'
import { onMounted, computed } from 'vue'
import Personalization from './components/Personalization.vue';
import { usePersonalizationDataStore } from '@/stores/personalizationData';
import { useDisplay } from 'vuetify'

const { setStatusMenuPersonalization, getStatusMenuPersonalization } = usePersonalizationDataStore()

const { name } = useDisplay()

const isNarrowScreen = computed(() => name.value == 'xs')
const statusMenu = computed(() => {
  return getStatusMenuPersonalization()
})

onMounted(() => {
  if(localStorage.getItem('personalization')){
    setStatusMenuPersonalization(false)
  }else{
    setStatusMenuPersonalization(true)
  }
})

</script>

<style lang="scss">
.closeStyle{
  text-decoration: none;
  color: inherit;
}
</style>
