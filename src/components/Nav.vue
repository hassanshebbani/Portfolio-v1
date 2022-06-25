<script setup lang="ts">
import { ref, onMounted } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import gsap from "gsap";
const navMenu = ref<HTMLDivElement>();
const navToggle = ref<HTMLDivElement>();
const navClose = ref<HTMLDivElement>();
const navIcons = ref<HTMLAnchorElement[]>();
const navLinks: { link: string; icon: string }[] = [
  { link: "Home", icon: "uil uil-estate" },
  { link: "About", icon: "uil uil-user" },
  { link: "Skills", icon: "uil uil-file-alt" },
  { link: "Services", icon: "uil uil-briefcase" },
  { link: "Portfolio", icon: "uil uil-scenery" },
  { link: "Contact", icon: "uil uil-message" },
];

const s = () => {
  document.querySelector("body")!.classList.add("dark-theme");
};

onMounted(async () => {
  navToggle.value!.addEventListener("click", () => {
    gsap.to(navMenu.value!, {
      duration: 0.2,
      bottom: "0%",
      ease: "power2.inOut",
    });
  });
  navClose.value!.addEventListener("click", () => {
    gsap.to(navMenu.value!, { bottom: "-100%" });
  });
  for (let i = 0; i < navIcons.value!.length; i++) {
    navIcons.value![i].addEventListener("click", () => {
      // swiper.slideTo(i, 1000, true);
      gsap.to(navMenu.value!, {
        bottom: "-100%",
        //   clipPath: "circle(20rem 100%)"
      });
    });
  }
  s();

});
</script>

<template>
  <header class="header" id="header">
    <nav class="nav container">
      <a href="#" class="nav-logo">Hassan Shebbani</a>
      <div class="nav-menu" ref="navMenu">
        <ul class="nav-list grid">
          <li v-for="(item, index) in navLinks" :key="index" class="nav-item">
            <a :href="`#${item.link.toLowerCase()}`" class="nav-link">
              <div class="nav-icon" ref="navIcons">
                <i :class="item.icon"></i
                ><span class="cursor-pointer">{{ item.link }}</span>
              </div>
            </a>
          </li>
        </ul>
        <i class="uil uil-times nav-close flex md:hidden" ref="navClose"></i>
      </div>
      <div class="nav-btns">
        <!-- Theme change button -->
        <i class="uil uil-moon change-theme" @click="s" ref="themeBtn"></i>
        <div class="nav-toggle" ref="navToggle">
          <i class="uil uil-apps md:hidden"></i>
        </div>
      </div>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
.active-link {
  color: cyan;
  transition: all 0.3s;
}
.header {
  width: 100%;
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 10;
  font-size: 2rem;
  .nav {
    @include flex(row, center, space-between);
    width: 80%;
    margin: auto;
  }
  .container {
    background: white;
    .nav-logo {
      &:hover {
        color: cyan;
      }
    }
    .nav-menu {
      // background: rgba(3, 202, 202, 0.486);
      backdrop-filter: blur(1rem);
      @media screen and (max-width: 767px) {
        position: fixed;
        bottom: -100%;
        left: 0;
        width: 100%;
        padding: 2rem 1.5rem 4rem;
        box-shadow: 0 -0.1rem 0.4rem rgba(0, 0, 0, 0.15);
        border-radius: 1.5rem 1.5rem 0 0;
        transition: 0.3s;
      }
      .nav-list {
        grid-template-columns: repeat(6, 1fr);
        @media screen and (max-width: 767px) {
          grid-template-columns: repeat(3, 1fr);
        }
        gap: 2rem;
        .nav-item {
          color: rgba(0, 0, 0, 0.5);
          .nav-link {
            @include flex(row, center, center);
            font-size: 1.2rem;
            .nav-icon {
              @include flex(column, center, center);
              width: fit-content;
              i {
                cursor: pointer;
                font-size: 1.8rem;
              }
              &:hover {
                color: cyan;
              }
            }
          }
        }
      }
      .nav-close {
        position: absolute;
        right: 1.3rem;
        bottom: 0.5rem;
        font-size: 2.5rem;
        cursor: pointer;
        color: rgb(0, 187, 187);
        &:hover {
          color: red;
        }
      }
    }
    .nav-btns {
      @include flex(row, center, center);
      i {
        cursor: pointer;
      }
      .change-theme {
        margin-right: 1rem;
      }
    }
  }
}
</style>
