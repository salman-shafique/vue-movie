<template>
  <div class="app-wrapper">
    <MainHeader />
    <SubHeader />
    <MainContent />
  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue';
import SubHeader from './components/SubHeader.vue';
import MainContent from './components/MainContent.vue';

export default {
  components: {
    MainHeader,
    SubHeader,
    MainContent
  }
};
</script>

<style>
.app-wrapper {
  background-color: #1c1c1c;
  color: white;
  min-height: 100vh;
}
</style>
