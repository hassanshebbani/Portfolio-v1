<script setup lang="ts">
import SwipeNavigationVue from "../SwipeNavigation.vue";
// Swiper
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/effect-creative";
import "swiper/css/autoplay";
import "swiper/css/scrollbar";
import { EffectCreative, Autoplay, Scrollbar } from "swiper";
import "swiper/css/pagination";
const modules = [EffectCreative, Autoplay, Scrollbar];

const testimonials: {
  clientName: string;
  clientPosition: string;
  clientImg: string;
  stars: number;
  testimony: string;
}[] = [
  {
    clientName: "Zack Snyder",
    clientPosition: "Product Manager",
    clientImg: "t1.jpg",
    stars: 5,
    testimony:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut maxime eveniet deserunt cumque sit animi nihil nobis possimus!",
  },
  {
    clientName: "Hannah Gloria",
    clientPosition: "Software Tester",
    clientImg: "t2.jpg",
    stars: 4,
    testimony:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut maxime eveniet deserunt cumque sit animi nihil nobis possimus!",
  },
  {
    clientName: "Rose Clinton",
    clientPosition: "Branding Ambassador",
    clientImg: "t3.jpg",
    stars: 2,
    testimony:
      "Lorem ipsum dolor sit amet consectetur!",
  },
  {
    clientName: "Jomaica Brunoz",
    clientPosition: "Talent Recruiter",
    clientImg: "t4.jpg",
    stars: 4,
    testimony: "Lorem ipsum dolor sit amet consectetur adipisicing elit!",
  },
];
</script>

<template>
  <!-- Testimonials Section -->
  <section class="testimonials-section">
    <h2>Don't Trust. <span>VERIFY.</span></h2>
    <h3 class="section-subtitle mb-10 md:mb-20">Checkout what my clients have to say about me :)</h3>
    <SwipeNavigationVue :mySwiperClass="'swiper-testimonials'"/>
    <div class="testimonials-container">
      <swiper
      :rewind="true"
        :scrollbar="{
          verticalClass: 'swiper-scrollbar-vertical',
        }"
        :autoplay="{
          disableOnInteraction: false,
          pauseOnMouseEnter: true,
        }"
        :grabCursor="true"
        :effect="'creative'"
        :creativeEffect="{
          prev: {
            opacity: 0,
            translate: [0, 0, -400],
          },

          next: {
            translate: ['100%', 0, 0],
          },
        }"
        :modules="modules"
        class="swiper-testimonials"
      >
        <swiper-slide
          v-for="(item, index) in testimonials"
          :key="index"
          class="content swiper-slide-testimonials"
        >
            <div class="testimony p-12">
              <!-- Testimony Top -->
              <div class="top">
                <span class="uil uil-cube"></span>
                <div class="stars">
                  <i
                    v-for="(_, i) in item.stars"
                    :key="i"
                    class="uis uis-star"
                  ></i>
                  <i
                    v-for="(_, i2) in 5 - item.stars"
                    :key="i2"
                    class="uil uil-star"
                  ></i>
                </div>
              </div>
              <!-- Testimony Middle -->
              <p>{{ item.testimony }}</p>
              <div class="bottom">
                <img
                  :src="`/assets/images/testimonials/${item.clientImg}`"
                  :alt="item.clientName"
                />
                <div class="bottom-details">
                  <h3>{{ item.clientName }}</h3>
                  <span>{{ item.clientPosition }}</span>
                </div>
              </div>
          </div>
        </swiper-slide>
      </swiper>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.testimonials-section {
  .testimonials-container {
    margin-top: 3rem;
    .content {
      @include flex(column, center, center);
      height: 100%;
        .testimony {
          @include flex(column, flex-start, space-between);
          width: 100%;
          .top {
            width: 100%;
            @include flex(row, center, space-between);
            span {
              font-size: 4rem;
            }
            .stars {
              justify-self: flex-end;
              @include flex(row, center, center);
              margin-left: auto;
              color: yellow;
              font-size: 2rem;
            }
          }
          
        p {
          font-size: 1.75rem;
          margin: 3rem 0;
          opacity: 1;
        }
          .bottom {
            @include flex(row, flex-start, space-between);
            img {
              width: 8rem;
              height: 8rem;
              border-radius: 50%;
              margin-right: 2rem;
              object-fit: contain;
            }
            .bottom-details {
              h3 {
                font-size:2rem;
                // font-weight: bold;
                margin-bottom: 0.5rem;
              }
              span {
                font-size: 1.5rem;
                color: rgb(1, 207, 207);
                // font-weight: bold;
                // opacity: 0.7;
              }
            }
          }
        }
      }
  }
}

.swiper-testimonials {
  width: clamp(10rem, 80vw, 78rem);
  // height: fit-content;
  // background: white;
}

.swiper-slide-testimonials {
  background: rgba(0, 0, 0, 0.4);
  border-radius: 2rem;
}
</style>
