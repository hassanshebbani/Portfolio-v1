<script setup lang="ts">
import SwipeNavigationVue from "../SwipeNavigation.vue";
// Swiper
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/effect-creative";
import "swiper/css/pagination";

import {
  EffectCreative,
  Pagination,
} from "swiper";
const modules = [EffectCreative, Pagination,];

const myPortfolio: {
  title: string;
  description: string;
  img: string;
  alt: string;
  link: string;
}[] = [
  {
    title: "Landing Page Concept",
    description:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur ullam, a, alias ea at possimus reprehenderit, assumenda modiomnis temporibus fugiat!",
    img: "hs-cwui-1-resize-760x401.png",
    alt: "Hassan Shebbani Concept Web UI 1",
    link: "https://hs-concept-web-ui-1.netlify.app",
  },
  {
    title: "Super Car Slide Show",
    description:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur ullam, a, alias ea at possimus reprehenderit.",
    img: "hs-cwui-2-resize-760x401.png",
    alt: "Hassan Shebbani Concept Web UI 2",
    link: "https://hs-cwui-2.netlify.app",
  },
];
</script>

<template>
  <!-- Portfolio Section -->
  <section class="portfolio-section" id="portfolio">
    <h2 class="text-center">Some of my recent work</h2>
    <SwipeNavigationVue :mySwiperClass="'swiper-portfolio'"/>
    <div class="portfolio-container">
      <!-- <div> -->
      <swiper
        :rewind="true"
        :grabCursor="true"
        :effect="'creative'"
        :pagination="{
          clickable: true,
          horizontalClass: 'swiper-pagination-horizontal',
          type: 'bullets',
        }"
        :creativeEffect="{
          prev: {
            shadow: false,
            opacity: 0,
            translate: ['-120%', 0, -500],
          },
          next: {
            shadow: false,
            opacity: 0,
            translate: ['120%', 0, -500],
          },
        }"
        :modules="modules"
        class="swiper-portfolio"
      >
        <swiper-slide
          v-for="(item, index) in myPortfolio"
          :key="index"
          class="content grid swiper-slide-portfolio"
        >
          <img :src="`/assets/images/${item.img}`" :alt="item.alt" />
          <div class="leading">
            <h3>{{ item.title }}</h3>
            <p>
              {{ item.description }}
            </p>
            <a class="cta activate-cursor" :href="item.link" target="_blank"
              >Demo <i class="activate-cursor uil uil-arrow-right"></i
            ></a>
          </div>
        </swiper-slide>
      </swiper>
    </div>
    <!-- </div> -->
  </section>
</template>

<style lang="scss" scoped>
.portfolio-section {
  .portfolio-container {
    overflow: initial;
    margin-top: 3rem;
    .content {
      margin-bottom: 5rem;
      img {
        width: 100%;
        border-radius: 1.5rem;
        box-shadow: 0 0.8rem 1rem rgba(0, 0, 0, 0.2);
        justify-self: center;
      }
      .leading {
        @include flex(column, flex-start, flex-start);
        h3 {
         font-size: clamp($medium-fs, 2vw, $big-fs);
          color: cyan;
          margin: 2rem 0 1rem;
        }
        p {
          font-size: clamp($small-fs, 2vw, $medium-fs);
          line-height: 3rem;
          opacity: 0.85;
        }
        .cta {
          @include flex(row, center, space-between);
          justify-self: flex-end;
          align-self: flex-end;
          transition: 0.3s all;
          i {
            display: block;
            margin-left: 1rem;
            transition: 0.3s all;
          }
          &:hover {
            transform: translateY(-0.5rem);
            transition: 0.3s all;
            i {
              transform: translateX(0.5rem);
              transition: 0.3s all;
            }
          }
        }
      }
    }
  }
}

.swiper-portfolio {
  width: clamp(10rem, 80vw, 100rem);
  height: fit-content;
}

.swiper-slide-portfolio {
  @include flex(column, center, center);
  padding: 0 0 2rem;
}
</style>
