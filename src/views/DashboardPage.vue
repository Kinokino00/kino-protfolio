<template>
  <div class="dashboard-all">
    <div class="photo-bg">
      <div class="photo-bg-inner">
        <div class="photo-bg-area"></div>

        <div v-if="menuItems[0].active" class="area area-work">
          <div class="area-line"></div>
          <div class="area-info" v-for="info in certificateItem" :key="info.ad">
            <p class="font-num min-w-[50px] text-end">
              <span class="number">{{ info.tenureYear }}</span>y
              <template v-if="info.tenureMonth">
                {{ info.tenureMonth }}m
              </template>
            </p>
            <div class="circle"></div>
            <div class="area-info-detail">
              <p class="font-num">{{ info.ad }}</p>
              <p class="text-lg">{{ info.job }}</p>
              <p v-if="info.jobAdjunct" class="-mt-1 opacity-80">{{ info.jobAdjunct }}</p>
              <p class="text-base">{{ info.company }}</p>
            </div>
          </div>
        </div>

        <div v-if="menuItems[1].active" class="area area-certificate">
          <div class="area-line"></div>
          <div class="area-info">
            <p class="area-info-label min-w-[88px]">Certificate</p>
            <div class="circle-detail">
              <div class="circle"></div>
              <div class="area-info-detail">
                <img class="TQC" src="@/assets/images/TQC.png" alt="TQC">
                <h2 class="text-xl">大數據分析專業人才</h2>
                <p>軟體開發知識</p>
                <p>網頁資料擷取與分析</p>
                <p>基礎程式語言</p>
              </div>
            </div>
          </div>
        </div>

        <div v-if="menuItems[2].active" class="area area-skill">
          <div class="area-line"></div>
          <div class="area-info" v-for="skills in skillItem" :key="skills.label">
            <p class="area-info-label">{{ skills.label }}</p>
            <div class="circle"></div>
            <div class="grid gap-1.5 2xl:gap-3">
              <div class="area-info-detail" v-for="(skill,i) in skills.text" :key="i">
                <i :class="skill"></i>
                <p>{{ skill }}</p>
              </div>
            </div>
          </div>
        </div>

        <div v-if="menuItems[3].active" class="area area-project">
          <div class="area-line"></div>
          <div class="area-info" v-for="projects in projectItem" :key="projects.label">
            <p class="area-info-label">{{ projects.label }}</p>
            <div class="circle"></div>
            <div class="grid gap-1.5 gap-3">
              <div class="area-info-detail" v-for="(project,i) in projects.text" :key="i">
                <p v-if="project.year" class="font-num">{{ project.year }}</p>
                <p class="text-base">{{ project.name }}</p>
              </div>
            </div>
          </div>
        </div>

        <div v-if="menuItems[4].active" class="area area-about">
          <p class="text-justify">
            　　具備一年 Python 學習背景，會使用 Django 框架及 Selenium、BeautifulSoup 套件，懂資料庫基本操作，已取得 TQC 大數據分析專業人才證照。<br><br>

            　　於前端專案中負責API串接，使用 Vue3 框架、TypeScript、Tailwindcss 和 Scss。此前參與了多個 APP 和 Web 專案的 UI 設計。<br><br>

            　　於擔任營業處督導期間，負責行銷企劃、規劃執行、人員管理與溝通協作，這些經驗培養了我良好的團隊合作和溝通能力。擅長跨部門協作，能有效地與團隊成員合作，達成專案目標。<br><br>

            　　我性格謙和、樂觀且活潑，致力於成為一名圓融通達的專業人才。
          </p>
        </div>

        <div v-if="allActive" class="photo-bg-kino"></div>
      </div>
    </div>
    <div class="title-menu">
      <div class="relative">
        <h1 class="title">Kino's<br>Portfolio</h1>
        <div class="title-light">Kino's<br>Portfolio</div>
      </div>
      <ul class="menu">
        <li v-for="(menu, index) in menuItems" :key="menu.label" class="menu-item" :class="{ 'active': menu.active }" @click="activeMenu(index)">
          <button>{{ menu.label }}</button>
          <div class="line"></div>
        </li>
      </ul>
    </div>
    <div class="border-bottom"></div>
  </div>
</template>


<script lang="ts" setup>
import { computed, ref } from 'vue'

interface MenuItem {
  label: string
  active: boolean
}
interface CertificateItem {
  tenureYear: number
  tenureMonth?: number
  ad: string
  job: string
  jobAdjunct?: string
  company: string
}

const menuItems = ref<MenuItem[]>([
  { label: 'Work Experience', active: false },
  { label: 'Certificate', active: false },
  { label: 'Skill', active: false },
  { label: 'Project & Side Project', active: false },
  { label: 'About Me', active: false }
])

const activeMenu = (index:number) => {
  menuItems.value.forEach((menu, i) => {
    menu.active = i === index
  })
}

const allActive = computed(() => menuItems.value.every(menu => !menu.active))

const certificateItem = ref<CertificateItem[]>([
  {
    tenureYear: 2,
    ad: '2022/05~',
    job: 'Front-End Developer',
    company: '樺康智雲股份有限公司',
  }, {
    tenureYear: 2,
    ad: '2020/04~2022/03',
    job: 'Front-End Developer',
    jobAdjunct: '& UI Designer',
    company: '登伴有限公司',
  }, {
    tenureYear: 1,
    tenureMonth: 10,
    ad: '2020/03~2022/03',
    job: 'UI Designer',
    jobAdjunct: '& Graphic Designer',
    company: '瑄品股份有限公司',
  }, {
    tenureYear: 1,
    tenureMonth: 8,
    ad: '2015/10~2017/05',
    job: '營業所督導',
    jobAdjunct: '& Graphic Designer',
    company: '錏洲娛樂機械有限公司',
  }
])

const skillItem = ref([
  {
    label: 'Back-end',
    text: [
      'Python', 'django', 'Selenium', 'BeautifulSoup'
    ]
  }, {
    label: 'Front-end',
    text: [
      'HTML', 'CSS', 'Vue', 'Javascript', 'Typescript'
    ]
  }, {
    label: 'UI Designer',
    text: [
      'Figma'
    ]
  }, {
    label: 'Graphic Designer',
    text: [
      'Illustrator', 'Photoshop'
    ]
  },
])

const projectItem = ref([
  {
    label: 'Back-end',
    text: [{ name: 'Meet Food' }]
  }, {
    label: 'Front-end',
    text: [{
        year: 2024,
        name: '能源管理系統'
      }, {
        year: 2021,
        name: '龍奉宮'
      }, {
        year: 2020,
        name: '台灣新計畫有限公司'
    }]
  }, {
    label: 'Front-end & UI',
    text: [{
        year: 2022,
        name: '樺晟科技股份有限公司'
      }, {
        year: 2022,
        name: 'Ttoper'
    }]
  },
])
</script>


<style lang="scss" scoped>
p {
  @apply text-xs md:text-sm;
}
.border {
  &-color {
    @apply border-white/15;
  }
  &-bottom {
    @apply absolute left-0 w-screen border-b border-color transition-all;
    @apply bottom-12 md:bottom-24 xl:bottom-16 2xl:bottom-44;
  }
}
.dashboard-all {
  @apply flex justify-between h-screen mr-9 border-r border-color transition-all md:mx-auto;
  @apply md:max-w-[80vw] xl:max-w-[70vw] 2xl:max-w-[70vw];
}
.photo-bg {
  @apply transition-all overflow-hidden;
  @apply w-[100vw] sm:w-[60vw] md:w-[48vw] lg:w-[40vw] xl:w-[20vw] 2xl:w-[30vw] 3xl:w-[26vw];

  &-inner {
    @apply relative flex flex-col items-center justify-center;
    @apply top-[42vh]       md:top-0;
    @apply -translate-y-1/2 md:translate-y-0;
    aspect-ratio: 9/16;
  }
  &-kino {
    @apply absolute top-0 left-0 w-full h-full;
    background-image: url('@/assets/images/Kino.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
  }
  &-area {
    @apply -z-10 absolute top-0 left-0 w-full h-full bg-white opacity-15 mix-blend-overlay;
  }
}
.area {
  @apply relative grid items-baseline justify-center gap-4 h-fit text-white text-sm;
  @apply px-10 xl:px-3;
  mask-image: linear-gradient(black 60%, #00000030);

  .number {
    @apply text-xl;
  }
  .circle {
    @apply relative min-w-2 max-w-2 min-h-2 bg-white rounded-full;
  }

  &-info {
    @apply flex items-baseline gap-2 2xl:gap-3;
    &-detail {
      @apply flex flex-col gap-1;
    }
    &-label {
      @apply relative text-base text-end font-bold md:text-lg;
    }
  }

  &-line {
    @apply absolute w-px h-full bg-white;
    mask-image: linear-gradient(black 80%, transparent);
  }

  &-work {
    .area-line {
      @apply top-4 left-[73px] 2xl:left-[77px];
    }
  }

  &-certificate {
    @apply relative whitespace-nowrap;
    .area {
      &-line {
        @apply top-10       xl:top-3;
        @apply left-[146px] xl:left-[15px];
      }
      &-info {
        @apply xl:flex-col xl:gap-0;
        &-label {
          @apply -top-7 xl:top-0 xl:left-5;
        }
        &-detail {
          @apply xl:ml-4;
        }
      }
    }
    .circle {
      @apply -top-7 xl:-top-4;
    }
    .TQC {
      @apply w-[140px] xl:w-[120px];
    }
  }

  &-skill, &-project {
    .area-info-label {
      @apply text-base 2xl:text-lg;
      @apply leading-5 2xl:leading-7;
    }
  }

  &-skill {
    @apply gap-3 2xl:gap-8;
    .circle, .area-info-label {
      @apply -top-2 2xl:-top-3;
    }
    .area {
      &-line {
        @apply left-[111px] 2xl:left-[206px];
        @apply top-4 2xl:top-5;
      }
      &-info {
        &:nth-last-of-type(2), &:nth-last-of-type(1) {
          .area-info-label {
            @apply 2xl:-top-5;
          }
        }
        &-label {
          @apply max-w-[88px] min-w-[88px] 2xl:min-w-[152px];
        }
        &-detail {
          @apply flex-row items-center gap-1;
          i {
            @apply bg-no-repeat bg-center bg-contain;
            @apply w-6 2xl:w-9;
            @apply h-6 2xl:h-9;
            $skills: 'Python', 'django', 'Selenium', 'BeautifulSoup','HTML', 'CSS', 'Vue', 'Javascript', 'Typescript', 'Figma', 'Illustrator', 'Photoshop';
            @each $skill in $skills {
              &.#{$skill} {
                background-image: url('@/assets/images/icon/#{$skill}.png');
              }
            }
            &.BeautifulSoup {
              @apply w-[40px] 2xl:w-[72px];
            }
          }
        }
      }
    }
  }

  &-project {
    .area {
      &-line {
        @apply top-4 2xl:top-5 left-[113px] 2xl:left-[186px];
      }
      &-info {
        &-label {
          @apply max-w-[90px] min-w-[90px] 2xl:min-w-[130px];
        }
        &-detail {
          @apply gap-0 2xl:gap-1;
        }
      }
    }
  }

  &-about {
    mask-image: none;
  }
}

.title-menu {
  @apply relative flex flex-col transition-all;
  @apply mr-4      sm:mr-4      md:mr-10;
  @apply mt-[4vh]               md:mt-[10vh] xl:mt-[7vh] 2xl:mt-[20vh];
  @apply mb-[10vh] sm:mb-[10vh] md:mb-[21vh] xl:mb-[15vh] 2xl:mb-[24vh];
}
.title {
  @apply leading-normal;
  @apply text-7xl xl:text-[48px] 2xl:text-[60px];

  &, &-light {
    @apply text-white font-black text-right mix-blend-overlay;
  }

  &-light {
    @apply absolute right-5 leading-[90%] opacity-10;
    @apply top-3 xl:top-6 2xl:top-5;
    @apply text-[60px] md:text-[70px] 2xl:text-[110px];
  }
}
.menu {
  @apply absolute bottom-0 flex flex-col items-end gap-4 font-medium text-white whitespace-nowrap;
  @apply right-0 md:-right-3;

  &-item {
    @apply flex items-center justify-end gap-2 w-fit text-lg opacity-50 hover:opacity-75;
    &:hover, &.active {
      @apply text-xl leading-[135%];
    }
    &.active {
      @apply relative mr-7 opacity-100;
      .line {
        @apply absolute -right-[19.5vw] w-[19vw];
      }
    }
  }
  .line {
    @apply w-5 h-0.5 bg-white rounded;
  }
}

// @media screen and (max-height: 1000px) {
//   .photo-bg {
//     @apply w-[22vw];
//   }
//   .border-bottom {
//     @apply bottom-32;
//   }
//   .title-menu {
//     @apply mb-[17vh];
//   }
//   .area {
//     @apply gap-3;
//   }
// }
// @media screen and (max-height: 860px) {
//   .photo-bg {
//     @apply w-[19vw];
//   }
//   .border-bottom {
//     @apply bottom-24;
//   }
//   .title-menu {
//     @apply mb-[15vh];
//   }
// }
</style>
