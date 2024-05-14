<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Top from '@/components/Top.vue'
import LeftCircle from '@/components/LeftCircle.vue'
import RightCircle from '@/components/RightCircle.vue'
import Bottom from '@/components/Bottom.vue'
</script>

<script>
export default {
  name: 'App',
  components: {
    RouterLink,
    RouterView,
    Top,
    LeftCircle,
    RightCircle,
  },
  data() {
    return {
      dark: false,
      windowWidth: 0,
      WindowHeight: 0,
      ipData: {
        ipv4: 'fetching...',
        country_name: 'unknown',
        city: 'unknown',
      },
    }
  },
  props: {
  },
  methods: {
    switchDark() {
      this.dark = !this.dark;
    },
    getWindowWidth() {
      this.windowWidth = window.innerWidth;
    },
    getWindowHeight() {
      this.WindowHeight = window.innerHeight;
    },
    calc1() {
      // 数学计算式，右侧最大的圆占用的高度
      return Math.sqrt(Math.pow(865, 2) - Math.pow(this.windowWidth - 700, 2)) - 100 + Math.max(0, (800 * 650 / this.windowWidth) - 650);
    },
    async fetchIPData() {
      try {
        // Fetch IP address
        const response = await fetch("https://api.ipify.org?format=json");
        const data = await response.json();
        this.ipData.ipv4 = data.ip;
        // Fetch location data
        const locationResponse = await fetch("https://ipapi.co/json/");
        const locationData = await locationResponse.json();
        this.ipData.country_name = locationData.country_name;
        this.ipData.city = locationData.city;
        console.log("[Ip] Finished.");
      } catch (error) {
        console.log("[Ip] Error fetching data:", error);
      }
    },
  },
  mounted() {
    // 动态获取窗口宽度
    this.getWindowHeight();
    this.getWindowWidth();
    window.addEventListener('resize', () => {
      this.getWindowHeight();
      this.getWindowWidth();
    });
    // 根据时间判断是否进入夜间模式
    this.dark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    if (!this.dark) {
      const timeHour = new Date().getHours();
      console.log(timeHour);
      if (timeHour < 8 || timeHour > 18) {
        this.dark = true;
      }
    }
    // 获取ip地址信息
    this.fetchIPData();
  },
  computed: {
    circleLeftTop() {
      const r = this.calc1();
      return 'top: ' + Math.max(r, 100) + 'px';
    },
    mainMinHeight() {
      const r = this.calc1();
      return 'min-height: ' + (Math.max(r, 0) + this.WindowHeight + 100) + 'px';
    },
  }
}
</script>

<template>
  <Top :class="{ 'dark-only-font': dark }" :windowWidth="windowWidth" :dark="dark" class="main-top"
    @change-dark="switchDark" style="z-index: 9100;"></Top>
  <div class="main" :class="{ dark: dark }" :style="mainMinHeight">
    <LeftCircle class="circle1" :style="circleLeftTop" :windowWidth="windowWidth" />
    <RightCircle class="circle2" :windowWidth="windowWidth" />
  </div>
  <Bottom :ipInfo="ipData"></Bottom>
</template>

<style scoped>
.circle1 {
  z-index: 200;
  position: absolute;
  left: -100px;
}

.circle2 {
  top: -200px;
  z-index: 100;
  position: absolute;
  right: -100px;
}

.main {
  position: absolute;
  left: 0;
  top: 0;
  min-width: 100vi;
  height: max-content;
  transition: color 1s ease-in-out, background 1s ease-in-out;
}

.main-top {
  z-index: 999;
  position: fixed;
  transition: color 1s ease-in-out;
}

.dark-only-font {
  color: #fff;
}

.dark {
  background-color: #333;
  color: #fff;
}

.circlel:hover, .circler:hover {
  opacity: 0.9;
}

.dark .circlel:hover, .dark .circler:hover {
  z-index: 9000;
}

a {
  transition: background 0.2s;
}
</style>
