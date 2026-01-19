<template>
  <div
    class="work-wp"
    @wheel="onScrollHandler"
    @touchstart="onTouchstartHandler"
    @touchend="onTouchendHandler"
  >
    <div class="work-area" :class="{ inited: isInited }">
      <div
        v-for="(group, groupIndex) in groupedItems"
        class="work-group"
        :class="[!(groupIndex % 2 === 0) ? 'odd' : 'even']"
        :key="groupIndex"
      >
        <div
          ref="workGroupInner"
          class="work-group-inner"
          :style="{
            transform: `translateY(${getScrollPosition(groupIndex)}px)`,
          }"
        >
          <button
            v-for="(work, index) in group"
            :key="work.name"
            class="work-card"
            :class="{
              [!(index % 2 === 0) ? 'odd' : 'even']: true,
              onHover: isHover(index),
              offHover: hoverIndex !== null && !isHover(index),
            }"
            :id="`workCard-${work.name}`"
            @mouseenter="onMouseEnterWorkCard(work, index)"
            @mouseleave="onMouseLeaveWorkCard()"
            @click="onClickWorkCard(work)"
            ref="workCards"
          >
            <div class="work-link-content">
              <div class="work-link-image">
                <img
                  ref="workCardImages"
                  :src="`/worksCards/${work.image}`"
                  @error="onImageError"
                  alt=""
                />
              </div>
            </div>
            <div class="work-title">
              <p :class="work.projectNameColor">{{ work.detail.title.replace(/<span[^>]*>.*?<\/span>/g, '') }}</p>
            </div>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed, watch, nextTick } from "vue";
import MobileDetect from "mobile-detect";
import worksSetting from "@/works-setting";
import router from "@/router";
import { useOfficialStore } from "@/stores/official";

const officialStore = useOfficialStore();
const mobileDetect = new MobileDetect(window.navigator.userAgent);
const isMobile = mobileDetect.mobile();
const isTablet = mobileDetect.tablet();
const isPotable = isMobile || isTablet;
const { worksSettingList } = worksSetting;
const workList = ref(worksSettingList.filter((item) => item.use));
const workCards = ref([]);
const isVisible = ref(workList.value.map(() => false));
const onShowCount = computed(() => isVisible.value.filter((v) => v).length);
const hoverIndex = ref(null);
const cardColumnCount = ref(0);
const isInited = ref(false);
const mobile = ref(false);

const workGroupInner = ref(null);
const workCardImages = ref(null);
// breakpoint for responsive
const breakpointCardCount = ref(1);
const breakpointSetting = {
  "extra-small": { cardCount: 1 },
  small: { cardCount: 2 },
  medium: { cardCount: 3 },
  large: { cardCount: 3 },
  xlarge: { cardCount: 4 },
  xxlarge: { cardCount: 4 },
  xxxlarge: { cardCount: 5 },
};
let breakpoints;

const currentBreakpoint = ref("");
const backgroundTypeSelect = ref(null);

// 컨테이너 엘리먼트 class="work-wp" 핸들러

const scrollPosition = ref(0);
const maxWorkGroupInnerHeight = ref(0);

const onScrollHandler = (e) => {
  const { deltaY } = e;

  scrollPosition.value = Math.max(
    Math.min(0, scrollPosition.value - deltaY / 1.5),
    -maxWorkGroupInnerHeight.value
  );

  clearInterval(window.autoScrollInterval);
  scrollCheckerAndStart();
};
const onTouchstartHandler = (e) => {
  scrollCheckerAndStop();
};
const onTouchendHandler = (e) => {
  scrollCheckerAndStart();
};

const onImageError = (event) => {
  event.target.src = `/worksCards/temp.jpg`;
};

const onClickWorkCard = (work) => {
  if (!work.link) return;

  router.push({
    path: work.link,
  });
  officialStore.updateHomeScrollPosition(scrollPosition.value);
};

const onMouseEnterWorkCard = (work, index) => {
  scrollCheckerAndStop();
};

const onMouseLeaveWorkCard = () => {
  backgroundTypeSelect.value = null;
  hoverIndex.value = null;
  scrollCheckerAndStart();
};

const backgroundGradientCheck = (gradient) => {
  return backgroundTypeSelect.value === gradient;
};

const isHover = (index) => {
  return index === hoverIndex.value;
};

const getCssVariable = (varName) => {
  return parseInt(
    getComputedStyle(document.documentElement).getPropertyValue(`--${varName}`),
    10
  );
};

const checkBreakpoint = () => {
  const breakpointsArrays = Object.entries(breakpoints);
  const width = window.innerWidth;
  let matchedBreakpoint = breakpointsArrays[breakpointsArrays.length - 1][0];

  for (const [breakpoint, maxWidth] of breakpointsArrays) {
    if (width <= maxWidth) {
      matchedBreakpoint = breakpoint;
      break; // 첫 번째로 매치되는 브레이크포인트에서 반복 종료
    }
  }
  currentBreakpoint.value = matchedBreakpoint;
  changeCardLayout(null, 1);
};

// watch
watch(currentBreakpoint, (newBreakpoint, oldBreakpoint) => {
  changeCardLayout(newBreakpoint);
});

// computed
const groupedItems = computed(() => {
  let groups = Array.from({ length: breakpointCardCount.value }, () => []);

  // workList.value.forEach((item, index) => {
  workList.value
    .filter((item) => item.link && item.link !== "")
    .forEach((item, index) => {
      groups[index % breakpointCardCount.value].push({
        ...item,
        ...{ originIndex: index },
      });
    });

  const maxCardCount = groups.reduce(
    (max, arr) => Math.max(max, arr.length),
    0
  );
  cardColumnCount.value = (maxCardCount / window.innerHeight).toFixed(2);
  return groups;
});

const changeCardLayout = (newBreakpoint, dbg) => {
  const breakpoint = newBreakpoint || currentBreakpoint.value;
  breakpointCardCount.value = breakpointSetting[breakpoint].cardCount;
  maxWorkGroupInnerHeight.value =
    workGroupInner.value[0].offsetHeight - window.innerHeight + 80;
};

const isOdd = (num) => {
  return num % 2 === 0;
};

const getScrollPosition = (groupIndex) => {
  return Math.max(
    Math.min(0, scrollPosition.value * (isOdd(groupIndex) ? 1.2 : 1)),
    -maxWorkGroupInnerHeight.value
  );
};

const scrollCheckerAndStop = () => {
  clearInterval(window.autoScrollInterval);
};
const scrollCheckerAndStart = () => {
  if (window.scrollTimer) {
    clearTimeout(window.scrollTimer);
  }

  window.scrollTimer = setTimeout(() => {
    startAutoScroll();
  }, 3000);
};

let scrollTopInterval;

const onKeyDownAtHomeView = (event) => {
  const pageHeight = window.innerHeight;
  const maxContentHeight = maxWorkGroupInnerHeight.value;

  clearInterval(scrollTopInterval);

  if (event.key === "Home") {
    scrollTopInterval = setInterval(() => {
      if (scrollPosition.value < 0) {
        scrollPosition.value -= Math.floor(scrollPosition.value / 10);
      } else {
        clearInterval(scrollTopInterval);
      }
    }, 10);
  }
  if (event.key === "End") {
    scrollTopInterval = setInterval(() => {
      if (scrollPosition.value > -maxContentHeight) {
        scrollPosition.value -= Math.floor(
          (maxContentHeight - scrollPosition.value) / 10
        );
      } else {
        clearInterval(scrollTopInterval);
      }
    }, 10);
  }
  if (event.key === "PageDown") {
    const targetScrollPosition = scrollPosition.value - pageHeight;
    scrollTopInterval = setInterval(() => {
      if (scrollPosition.value > targetScrollPosition) {
        scrollPosition.value += Math.floor(
          (targetScrollPosition - scrollPosition.value) / 10
        );
      } else {
        clearInterval(scrollTopInterval);
      }
    }, 10);
  }
  if (event.key === "PageUp") {
    const targetScrollPosition = scrollPosition.value + pageHeight;
    scrollTopInterval = setInterval(() => {
      if (scrollPosition.value < targetScrollPosition) {
        scrollPosition.value -= Math.floor(
          (scrollPosition.value - targetScrollPosition) / 10
        );
      } else {
        clearInterval(scrollTopInterval);
      }
    }, 10);
  }
};

function startAutoScroll() {
  console.log('startAutoScroll');
  if (window.autoScrollInterval) {
    clearInterval(window.autoScrollInterval);
  }

  if (!isPotable) {
    window.autoScrollInterval = setInterval(() => {
      scrollPosition.value -= 0.12;
    }, 1);
  } else {
    window.autoScrollInterval = setInterval(() => {
      window.scrollBy(0, 2); 
      // scrollTo({ top: scrollY + 2 });
    }, 20);
  }
}

onMounted(() => {
  const officialStore = useOfficialStore();

  // 홈에서의 이전 스크롤 위치
  if (officialStore.homeScrollPosition) {
    const isLogoClick = officialStore.lastActionToHome === 'logo'
    scrollPosition.value = isLogoClick ? 0 : officialStore.homeScrollPosition;
  }

  window.addEventListener("keydown", onKeyDownAtHomeView);

  setTimeout(() => {
    isInited.value = true;
  }, 300);

  const breakpointNames = Object.keys(breakpointSetting);
  breakpoints = breakpointNames.reduce((acc, name) => {
    acc[name] = getCssVariable(name);
    return acc;
  }, {});

  window.addEventListener("resize", checkBreakpoint);

  const imageElements = workCardImages.value;
  const promises = imageElements.map(
    (img) =>
      new Promise((resolve) => {
        img.onload = resolve;
      })
  );

  Promise.all(promises).then(() => {
    checkBreakpoint();
    nextTick(() => {
      changeCardLayout(null, 1);
      scrollCheckerAndStart();
    });
  });
});

onUnmounted(() => {
  window.removeEventListener("resize", checkBreakpoint);
  window.removeEventListener("keydown", onKeyDownAtHomeView);
  clearInterval(window.autoScrollInterval);
  clearTimeout(window.scrollTimer);
});
</script>

<style scoped></style>
