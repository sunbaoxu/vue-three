<template>
    <vue-displacement-slideshow
            :images="images"
            displacement="require('../assets/logo.png')"
            :intensity="0.2"
            :speedIn="1.4"
            :speedOut="1.4"
            ease="Expo.easeInOut"
            class="vue-displacement-slideshow"
            ref="slideshow"></vue-displacement-slideshow>
</template>

<script>
import VueDisplacementSlideshow from "vue-displacement-slideshow";
export default {
  data (){
    return {
      timer:null
    }
  },
  components: {
    VueDisplacementSlideshow,
  },
  computed: {
    images() {
      return [
        require("../assets/1.jpg"),
        require("../assets/2.jpg"),
        require("../assets/3.jpg")
      ];
    }
  },
  methods: {
    init() {
      //We loop through all our images by calling the 'next' method of our component every 2 seconds
      this.timer = setInterval(() => {
        this.$refs.slideshow.next();
      }, 2000);
    }
  },
  mounted() {
    this.init();
  },
  beforeDestroy (){
    clearInterval(this.timer)
  }
};
</script>
<style>
.vue-displacement-slideshow{
  min-height: 500px;
}
</style>
