<script setup lang="ts">
import { ref, onMounted, VueElement } from "vue";
import HomeVue from "./components/sections/Home.vue";
import SkillsVue from "./components/sections/Skills.vue";
import QualificationsVue from "./components/sections/Qualifications.vue";
import ServicesVue from "./components/sections/Services.vue";
import PortfolioVue from "./components/sections/Portfolio.vue";
import TestimonialsVue from "./components/sections/Testimonials.vue";
import ContactVue from "./components/sections/Contact.vue";
import BgVue from "./components/Three/Bg.vue";
import gsap from "gsap";
import { Swiper, SwiperSlide } from "swiper/vue";
import { EffectCreative, FreeMode, Mousewheel, Scrollbar } from "swiper";
// Import Swiper styles
import "swiper/css";
import "swiper/css/free-mode";
import "swiper/css/scrollbar";
import "swiper/css/effect-creative";

const modules = [FreeMode, Scrollbar, Mousewheel, EffectCreative];
const myCursor = ref<HTMLDivElement>();
const activateNavSections = () => {
  const navSections = document.querySelectorAll(
    "section[id]"
  )! as NodeListOf<HTMLDivElement>;
  const scrollY = window.scrollY;
  for (let i = 0; i < navSections.length; i++) {
    const sectionHeight = navSections[i].offsetHeight;
    const sectionTop = navSections[i].offsetTop - 350;
    const sectionId = navSections[i].getAttribute("id");
    if (scrollY > sectionTop && scrollY <= sectionTop + sectionHeight) {
      document
        .querySelector(`.nav-menu a[href*='${sectionId}']`)!
        .classList.add("active-link");
    } else {
      document
        .querySelector(`.nav-menu a[href*='${sectionId}']`)!
        .classList.remove("active-link");
    }
  }
};
const activateAnimation = ref(0);
const canvasSlide = () => {
  activateAnimation.value += 1;
};

const activeCursor = (e: Event) => {
  const cursorDot = myCursor.value!.children[0] as HTMLDivElement;
  const cursorText = myCursor.value!.children[1] as HTMLSpanElement;
  const cursorDash = myCursor.value!.children[2] as HTMLSpanElement;
  const item = e.target as HTMLElement;
  if (item.classList.contains("activate-cursor")) {
    gsap.to(myCursor.value!, {
      duration: 0.25,
      scale: 2.5,
      background: "rgba(0, 0, 0, 0.4)",
      border: "none",
    });
    gsap.to(cursorDot, { duration: 0.2, opacity: 0 });
    gsap.to(cursorDash, {
      duration: 0.2,
      opacity: 1,
      display: "flex",
      boxShadow:
        "0 0.5rem 2rem rgba(0, 255, 255, 0.204), 0 -0.5rem 4rem rgba(0, 255, 255, 0.41)",
    });
    cursorText.innerText = "Click";
  } else {
    gsap.to(cursorDot, { duration: 0.2, opacity: 1 });
    gsap.to(myCursor.value!, {
      duration: 0.25,
      scale: 1,
      background: "transparent",
      border: "0.12rem solid rgba(255, 255, 255, 0.4)",
    });
    gsap.to(cursorDash, { duration: 0.2, opacity: 0, display: "none" });
    cursorText.innerText = "";
  }
};

onMounted(async () => {
  window.addEventListener("scroll", activateNavSections);
  window.addEventListener("mousemove", (e) => {
    myCursor.value!.style.top = e.pageY + "px";
    myCursor.value!.style.left = e.pageX + "px";
  });
  window.addEventListener("mouseover", activeCursor);
});
</script>

<template>
  <div class="myCursor" ref="myCursor">
    <div class="dot"></div>
    <span class="cursor-text"> </span>
    <div class="dash"></div>
  </div>
  <BgVue :animate-canvas="activateAnimation" />
  <swiper
    v-on:before-transition-start="canvasSlide"
    :effect="'creative'"
    :creativeEffect="{
      prev: {
        shadow: true,
        opacity: 0,
        translate: [0, 0, -400],
      },
      next: {
        translate: ['100%', 0, 0],
      },
    }"
    :grabCursor="true"
    :mousewheel="true"
    :direction="'horizontal'"
    :modules="modules"
    class="mySwiper"
  >
    <swiper-slide><HomeVue /></swiper-slide>
    <swiper-slide><QualificationsVue /></swiper-slide>
    <swiper-slide style="overflow: auto !important; height: auto !important">
      <SkillsVue />
    </swiper-slide>
    <swiper-slide><ServicesVue /></swiper-slide>
    <swiper-slide><PortfolioVue /></swiper-slide>
    <swiper-slide><TestimonialsVue /></swiper-slide>
    <swiper-slide><ContactVue /></swiper-slide>
  </swiper>
</template>

<style lang="scss" scoped>
.myCursor {
  @include flex(row, center, center);
  @media screen and (max-width: 500px) {
    display: none;
  }
  background: transparent;
  border-radius: 50%;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  width: 4rem;
  height: 4rem;
  border: 0.12rem solid rgba(255, 0, 0, 0.4);
  transform: translate(-50%, -50%);
  transform-origin: 75% 75%;
  z-index: 10;
  pointer-events: none;
  transition: all 0.05s;
  z-index: 2;
  .dash {
    display: none;
    width: 4rem;
    height: 4rem;
    border-radius: 50%;
    position: relative;
    &::before,
    &::after {
      content: "";
      position: absolute;
      inset: 0.3rem;
      border: 0.1rem solid transparent;
      border-right-color: rgba(0, 255, 255, 0.384);
      border-left-color: rgba(0, 255, 255, 0.356);
      border-radius: 50%;
      z-index: -1;
      animation: rotateBorder 3s infinite linear;
      @keyframes rotateBorder {
        from {
          transform: rotate(0deg);
        }
        to {
          transform: rotate(360deg);
        }
      }
    }
  }
  .cursor-text {
    font-size: 1rem;
    position: absolute;
    color: white;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-shadow: 0.1rem 0 cyan, -0.1rem 0 red;
  }
  .dot {
    position: absolute;
    border-radius: 50%;
    width: 0.45rem;
    height: 0.45rem;
    background: rgba(0, 247, 255, 0.705);
  }
}
.swiper {
  height: 100vh;
}

.swiper-slide {
  cursor: none;
  @media screen and (max-width: 500px) {
    cursor: auto;
  }
  height: 100%;
  overflow: auto !important;
}
</style>
