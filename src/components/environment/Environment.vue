<template>
  <div id="environment">
    <div id="backgroud" class="background">
      <div class="backcolors"></div>
      <div class="back"></div>

      <div id="ground" class="groundp" style="animation-play-state:paused">
        <div v-for="(n, index) in floors0" :key="index" 
        :class="{floor1:1==n,floor2:2==n,floor3:3==n,}">
        </div>
      </div>
      <div id="groundrp" class="groundrp1" style="animation-play-state:paused">
        <div v-for="(n, index) in floors" :key="index" 
        :class="{floor1:1==n,floor2:2==n,floor3:3==n,}">
        </div>
      </div>
      <div id="groundrp2" class="groundrp1 groundrp2" style="animation-play-state:paused">
        <div v-for="(n, index) in floors" :key="index" 
        :class="{floor1:1==n,floor2:2==n,floor3:3==n,}">
        </div>
      </div>
      <div id="groundrp3" class="groundrp1 groundrp3" style="animation-play-state:paused">
        <div v-for="(n, index) in floors" :key="index" 
        :class="{floor1:1==n,floor2:2==n,floor3:3==n,}">
        </div>
      </div>
      <div id="groundrp4" class="groundrp1 groundrp4" style="animation-play-state:paused">
        <div v-for="(n, index) in floors" :key="index" 
        :class="{floor1:1==n,floor2:2==n,floor3:3==n,}">
        </div>
      </div>
      
      
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'Environment',
  data() {
    return {
      floors0: [
        2, 2, 2, 2, 2, 2, 2, 3, 1, 2, 
        2, 2, 3, 1, 2, 2, 2, 2, 2, 2, 
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
        2, 2, 2, 2, 2, 2, 2, 3, 1, 2, 
        2, 2, 3, 1, 2, 2, 2, 2, 2, 2, 
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
        2, 2, 2, 2, 2, 2, 2, 3, 1, 2, 
        2, 2, 3, 1, 2, 2, 2, 2, 2, 2, 
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
      ],
      floors: [
        2, 2, 2, 2, 2, 2, 2, 3, 1, 2, 
        2, 2, 3, 1, 2, 2, 2, 2, 2, 2, 
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
        2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]
    }
  }
}
</script>

<style scoped>
@import './environment.css';

</style>