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
            <div class="circle"></div>
            <div class="area-info-detail">
              <img src="@/assets/images/TQC.png" alt="TQC">
              <h2 class="text-xl">大數據分析專業人才</h2>
              <p>軟體開發知識</p>
              <p>網頁資料擷取與分析</p>
              <p>基礎程式語言</p>
            </div>
          </div>
        </div>

        <!-- <div v-if="menuItems[2].active" class="area area-skill"> -->
        <div class="area area-skill">
          <div class="area-line"></div>

          <div class="area-info" v-for="skills in skillItem" :key="skills.label">
            <p class="area-info-label">{{ skills.label }}</p>
            <div class="circle"></div>
            <div class="grid gap-4">
              <div class="area-info-detail" v-for="(skill,i) in skills.text" :key="i">
                <i :class="skill"></i>
                <p class="text-lg">{{ skill }}</p>
              </div>
            </div>
          </div>
        </div>

        <div v-if="menuItems[3].active" class="area area-project"></div>

        <div v-if="menuItems[4].active" class="area area-about"></div>

        <!-- <div v-if="allActive" class="photo-bg-kino"></div> -->
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
    ],
  },
  // {
  //   label: 'Front-end',
  //   text: [
  //     'Python', 'django', 'Selenium', 'BeautifulSoup'
  //   ],
  // },
])
</script>


<style lang="scss" scoped>
.border {
  &-color {
    @apply border-white/15;
  }
  &-bottom {
    @apply absolute left-0 w-screen border-b border-color transition-all;
    @apply bottom-12 md:bottom-24 xl:bottom-32 2xl:bottom-44;
  }
}
.dashboard-all {
  @apply flex justify-between h-screen mr-9 border-r border-color transition-all md:mx-auto;
  @apply md:max-w-[80vw] 2xl:max-w-[70vw];
}
.photo-bg {
  @apply transition-all overflow-hidden;
  @apply w-[34vw] md:w-[23vw] xl:w-[27vw] 2xl:w-[23.5vw];

  &-inner {
    @apply relative grid items-center justify-center;
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
  @apply relative flex flex-col items-baseline justify-center gap-4 px-10 h-fit text-white text-sm;
  mask-image: linear-gradient(black 60%, #00000030);

  .number {
    @apply text-xl;
  }
  .circle {
    @apply relative min-w-2 min-h-2 bg-white rounded-full;
  }

  &-info {
    @apply flex items-baseline gap-3;
    &-detail {
      @apply flex flex-col gap-1;
    }
    &-label {
      @apply relative text-lg text-end font-bold;
    }
  }

  &-line {
    @apply absolute w-px h-full bg-white;
    mask-image: linear-gradient(black 80%, transparent);
  }

  &-work {
    .area-line {
      @apply top-4 left-[104px];
    }
  }

  &-certificate {
    .area-line {
      @apply top-6 left-[143px];
    }
    .circle, .area-info-label {
      @apply -top-4;
    }
  }

  &-skill {
    @apply gap-8;
    .circle {
      @apply top-0;
    }
    .area {
      &-line {
        @apply top-0 left-[176px];
      }
      &-info {
        &-label {
          @apply min-w-[120px];
        }
        &-detail {
          @apply flex-row items-center gap-1;
          i {
            @apply w-9 h-9;
            $skills: 'Python', 'django', 'Selenium', 'BeautifulSoup';
            @each $skill in $skills {
              &.#{$skill} {
                background-image: url('@/assets/images/#{$skill}.png');
              }
            }
            &.BeautifulSoup {
              @apply w-[72px];
            }
          }
        }
      }
    }
  }

  &-project {}

  &-about {}
}

.title-menu {
  @apply relative flex flex-col transition-all;
  @apply mr-4      sm:mr-4      md:mr-10;
  @apply mt-[8vh]               md:mt-[10vh] xl:mt-[15vh] 2xl:mt-[20vh];
  @apply mb-[10vh] sm:mb-[10vh] md:mb-[21vh] xl:mb-[18vh] 2xl:mb-[24vh];
}
.title {
  @apply leading-normal;
  @apply text-7xl xl:text-[60px];

  &, &-light {
    @apply text-white font-black text-right mix-blend-overlay;
  }

  &-light {
    @apply absolute right-5 leading-[90%] opacity-10;
    @apply top-3 xl:top-5;
    @apply text-[60px] md:text-[70px] xl:text-[110px];
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

</style>
