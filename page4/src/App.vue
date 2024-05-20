<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Top from '@/components/Top.vue'
import LeftCircle from '@/components/LeftCircle.vue'
import RightCircle from '@/components/RightCircle.vue'
import GlobalSearch from '@/components/GlobalSearch.vue'
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
    GlobalSearch,
    Bottom,
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
      linkPages: [
        // 常用（请保持常用的索引为0）
        [
          { u: "https://chat.openai.com/chat", n: "ChatGPT", },
          { u: "https://github.com/", n: "Github", },
          { u: "https://singlelogin.se/", n: "ZLibrary", },
          { n: 'Gmail', u: 'https://mail.google.com/' },
          { n: 'QQmail', u: 'https://mail.qq.com/' },
          // 给中文网站创建en字段，方便拼音或英文替代搜索
          { n: '菜鸟教程', u: 'https://www.runoob.com/', en: "runoobcainiaojiaocheng", },
          { n: "WHU图书馆", u: "https://www.lib.whu.edu.cn/", en: "whulibrarywhutushuguan", },
          { n: 'WHU信息门户', u: 'https://ehall.whu.edu.cn/new/index.html#/', en: "whuxinximenhu", },
          { n: 'Leetcode', u: 'https://leetcode.cn/problemset/all/' },
          { n: 'iiiLab', u: 'https://bili.iiilab.com/' },
          { n: "高德地图", u: 'https://ditu.amap.com/', en: "gaodedituimap", },
          { n: "Bilibili", u: 'https://www.bilibili.com/', },
          { n: "雀魂麻将", u: 'https://game.maj-soul.net/1/', en: "quehunmajiangmajsoul", },
          { n: "Steam历史价格", u: 'https://steamdb.info/', en: "steamlishijiage", },
          { n: "科学上网", u: 'https://ikuuu.org/', en: "ikuuukexueshangwang", },
        ], 
        // 学习
        [
          { u: "https://chat.openai.com/chat", n: "ChatGPT", },
          { u: "https://github.com/", n: "Github", },
          { u: "https://singlelogin.se/", n: "ZLibrary", },
          { n: 'Leetcode', u: 'https://leetcode.cn/problemset/all/' },
          { n: "WHU图书馆", u: "https://www.lib.whu.edu.cn/", en: "whulibrarywhutushuguan", },
          { n: 'WHU信息门户', u: 'https://ehall.whu.edu.cn/new/index.html#/', en: "whuxinximenhu", },
          { n: "馆藏查询", u: 'http://opac.lib.whu.edu.cn/F/', en: "whuguancangchaxun"},
          { n: "给分查询", u: "https://s.ringjoys.com/", en: "geifenchaxunchageifen" },
          { n: "教务系统", u: "https://jwgl.whu.edu.cn/", en: "jiaowuxitong" },
          { n: "成绩单", u: "https://kxdz.whu.edu.cn", en: "chengjidan" },
          { n: "OpenWHU", u: "https://github.com/openwhu/OpenWHU/", en: "openwhu" },
          { n: "希冀平台", u: "https://cslabcg.whu.edu.cn/indexcs/simple.jsp?loginErr=0", en: "xijipingtaicglab" },
          { n: "蹭课助手", u: "https://cengkehelper.top/", en: "cengkezhushoucengkehelper" },
          { n: "Google翻译", u: "https://translate.google.com/", en: "googletranslate" },
          { n: "Annas", u: "https://annas-archive.org/", en: "annas" },
          { n: "易书网", u: "https://nav.yibook.org/", en: "yishuwangyibook" },
        ],
        // 文档
        [
          { n: '菜鸟教程', u: 'https://www.runoob.com/', en: "runoobcainiaojiaocheng", },
          { n: '维基百科', u: 'https://zh.wikipedia.org/zh-hans/', en: "wikipedia", },
          { n: 'W3School', u: 'https://www.w3schools.com/', },
          { n: 'MDN', u: 'https://developer.mozilla.org/zh-CN/', },
          { n: 'StackOverflow', u: 'https://stackoverflow.com/', },
          { n: 'C', u: 'https://www.w3schools.com/c/', }, 
          { n: 'C++', u: 'https://docs.microsoft.com/zh-cn/cpp/', en:'cppcplusplus'},
          { n: 'C#', u: 'https://docs.microsoft.com/zh-cn/dotnet/csharp/', en:'csharp'},
          { n: 'Python', u: 'https://docs.python.org/zh-cn/3/', },
          { n: 'Java', u: 'https://docs.oracle.com/javase/8/docs/api/', },
          { n: 'JavaScript', u: 'https://developer.mozilla.org/zh-CN/docs/Web/JavaScript', },
          { n: 'HTML', u: 'https://developer.mozilla.org/zh-CN/docs/Web/HTML', },
          { n: 'CSS', u: 'https://developer.mozilla.org/zh-CN/docs/Web/CSS', },
          { n: 'SQL', u: 'https://docs.microsoft.com/zh-cn/sql/t-sql/language-reference?view=sql-server-ver16', en:'sqlsqlserver'},
          { n: 'Markdown', u: 'https://www.markdownguide.org/basic-syntax/', en:'markdown'},
          { n: 'LaTeX', u: 'https://www.latex-project.org/', en:'latex'},
          { n: 'Git', u: 'https://git-scm.com/', },
          { n: 'Node.js', u: 'https://nodejs.org/en/', },
          { n: 'npm', u: 'https://www.npmjs.com/', },
          { n: 'cnpm', u: 'https://npmmirror.com/', },
          { n: 'Yarn', u: 'https://yarnpkg.com/', },
          { n: 'Vue', u: 'https://cn.vuejs.org/', },
          { n: 'Vite', u: 'https://vitejs.dev/', },
          { n: 'Vue Router', u: 'https://router.vuejs.org/zh/', en: 'vueroutervue-router,'},
          { n: 'Vuex', u: 'https://vuex.vuejs.org/zh/', en: 'vuexvue-x'},
          { n: 'Element UI', u: 'https://element-plus.gitee.io/zh-CN/', en: 'elementui'},
          { n: 'React', u: 'https://react.dev/', },
          { n: 'Express', u: 'https://expressjs.com/zh-cn/', en: 'express'},
          { n: 'NestJS', u: 'https://docs.nestjs.com/', en: 'nestjs'},
          { n: 'Springboot', u: 'https://spring.io/projects/spring-boot', }, 
          { n: 'Django', u: 'https://docs.djangoproject.com/en/4.2/'},
          { n: 'Flask', u: 'https://flask.palletsprojects.com/en/2.3.x/', },
          { n: 'MySQL', u: 'https://dev.mysql.com/doc/', en: 'mysql'},
          { n: 'Sqlite3', u: 'https://www.sqlite.org/docs.html', }, 
          { n: 'MongoDB', u: 'https://www.mongodb.com/docs/', en: 'mongodb'},
          { n: 'Redis', u: 'https://redis.io/docs/', },
          { n: 'Docker', u: 'https://docs.docker.com/', },
          { n: 'Kubernetes', u: "https://kubernetes.io/zh-cn/", },
        ],
        // 工具
        [
          { n: "iKuuu", u: "https://ikuuu.org/", en: "ikuuu" },
          { n: "Freefq", u: "https://github.com/freefq/free", en: "freefq" },
          { n: "Steamdb", u: "https://steamdb.info/", en: "steamdb" },
          { n: "公众号", u: "https://mp.weixin.qq.com/", en: "gongzhonghao" },
          { n: "iiilab下载站", u: "https://bili.iiilab.com/", en: "iiilab" },
          { n: "Gmail", u: "https://mail.google.com/", en: "gmail" },
          { n: "高德地图", u: "https://ditu.amap.com/", en: "gaode" },
          { n: "QQ邮箱", u: "https://mail.qq.com/", en: "qqmail" },
          { n: "雀魂", u: "https://game.maj-soul.net/1/", en: "quhun" },
          { n: "围棋对战", u: "https://online-go.com/", en: "weiqi_duizhan" },
          { n: "101围棋", u: "https://www.101weiqi.com/", en: "101weiqi" },
          { n: "YouTube", u: "https://www.youtube.com/", en: "youtube" },
          { n: "Twitter", u: "https://twitter.com/", en: "twitter" },
          { n: "Bilibili", u: "https://www.bilibili.com/", en: "bilibili" },
        ],
      ],
      linkTitles: [
        '常用',
        '学习',
        '文档',
        '工具',
      ],
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
    <RightCircle class="circle2" :windowWidth="windowWidth" :linkPages="linkPages" :linkTitles="linkTitles" />
    <GlobalSearch :windowWidth="windowWidth" :insitePages="linkPages" />
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

.circlel:hover,
.circler:hover {
  opacity: 0.9;
}

.dark .circlel:hover,
.dark .circler:hover {
  z-index: 9000;
}

a {
  transition: background 0.2s;
}
</style>
