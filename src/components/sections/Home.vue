<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
import SocialsVue from "../../components/Socials.vue";
const romanNums = ref<HTMLDivElement>(),
  firstName = ref<HTMLDivElement>(),
  lastName = ref<HTMLDivElement>();
const parallaxTextShadow = (e: any) => {
  const spans = romanNums.value?.getElementsByTagName(
    "span"
  )! as HTMLCollectionOf<HTMLSpanElement>;
  const x = e.clientX;
  const y = e.clientY;
  for (let i = 0; i < spans.length; i++) {
    spans[i].style.textShadow = `-${x * 0.001}rem ${
      y * 0.001
    }rem rgba(255, 0, 0, 0.062), ${x * 0.001}rem -${
      y * 0.001
    }rem rgba(0, 255, 255, 0.062)`;
  }
};
const animateMyName = async () => {
  const hassan = firstName.value!.children as HTMLCollection;
  const shebbani = lastName.value!.children;
  const nameTimeline: GSAPTimeline = gsap.timeline({
    defaults: {
      duration: 0.2,
      // ease: "power2.inOut",
    },
  });
  while (true) {
    for (let i = 0; i < hassan.length; i++) {
      await nameTimeline.fromTo(
        hassan[i] as HTMLSpanElement,
        { color: "rgba(0,0,0,0.4)" },
        { color: "rgb(22, 213, 219)" }
      );
    }
    for (let i = 0; i < shebbani.length; i++) {
      await nameTimeline.fromTo(
        shebbani[i] as HTMLSpanElement,
        { color: "rgba(0,0,0,0.4)" },
        { color: "rgb(22, 213, 219)" }
      );
    }
    await gsap.to(hassan, { duration: 5 });
    gsap.to(hassan, { duration: 0.5, color: "rgba(0, 0, 0, 0.4)" });
    await gsap.to(shebbani, {
      duration: 0.5,
      color: "rgba(0, 0, 0, 0.4)",
    });
  }
};
onMounted(async () => {
  window.addEventListener("mousemove", parallaxTextShadow);
  animateMyName();
});
</script>
<template>
  <!-- Home Section -->
  <section class="section" id="home">
    <div
      class="home-container relative min-h-screen w-full flex flex-col items-center justify-center"
    >
    <!-- Top -->
      <div
        class="top w-full flex items-start justify-between"
      >
        <div class="top-left hidden sm:flex flex-col">
          <h3>Full Stack Web & Android Development</h3>
          <h3>Web & Android Design</h3>
          <h3>Interactive Design</h3>
        </div>
        <div class="top-right">
          <h3 class="text-cyan-400">@hassan_shebbani/~ :</h3>
        </div>
      </div>
      <!-- Roman Numbers -->
      <div
        class="roman-nums w-full absolute top-10 md:relative grid grid-cols-2 gap-10 lg:gap-52 lg:mt-40"
        ref="romanNums"
      >
        <div class="left-rn flex items-center justify-between">
          <span
            v-for="(num, index) in ['I', 'II', 'III', 'IV', 'V']"
            :key="index"
          >
            {{ num }}
          </span>
        </div>
        <div class="right-rn flex items-center justify-between">
          <span
            v-for="(num, index) in ['VI', 'VII', 'VIII', 'IX', 'X']"
            :key="index"
          >
            {{ num }}
          </span>
        </div>
      </div>
      <!-- Middle -->
      <div
        class="middle w-full flex flex-col lg:flex-row items-center justify-center lg:justify-between"
      >
        <div class="my-name" ref="firstName">
          <span v-for="(char, index) in 'HASSAN'" :key="index">
            {{ char }}
          </span>
        </div>
        <img src="/assets/images/rdj.png" alt="" class="" />
        <div class="my-name" ref="lastName">
          <span v-for="(char, index) in 'SHEBBANI'" :key="index">
            {{ char }}
          </span>
        </div>
      </div>
      <br class="flex md:hidden">
      <!-- Bottom -->
      <div class="bottom w-full relative flex flex-col md:flex-row items-center md:items-start justify-between">
        <div class="bottom-left flex-1">
          <h2 class="xl:w-1/2">About Me</h2>
          <p class="w-full xl:w-2/3">
            I’m Hassan Shebbani a graduate from the Lebanese International
            University. I LOVE coding & designing visually & highly performant
            websites & apps!
          </p>
        </div>
        <div
          class="bottom-right flex flex-1 items-center justify-end"
        >
          <a
            class="activate-cursor mt-10 lg:mr-40"
            href="/sample-pdf.pdf"
            download=""
            target="_blank"
          >
            <div class="my-resume activate-cursor">RESUME</div>
          </a>
        </div>
      </div>
    <SocialsVue
      class="mt-10 lg:mb-10 lg:mt-0"
      :all-class="'flex flex items-center justify-center'"
      :single-class="'mx-10'"
    />
    <br>
    </div>
  </section>
</template>
<style lang="scss" scoped>
.home-container {
  overflow-x: hidden;
  gap: 1rem;
  align-items: center;
  .top {
    h3 {
      font-size: 1.75rem;
      opacity: 0.3;
      margin-bottom: 2rem;
    }
  }
  .roman-nums {
    span {
      font-size: clamp($medium-fs, 2vw, $big-fs);
      color: rgba(255, 255, 255, 0.1);
      text-shadow: 0.5rem 0 rgba(255, 0, 0, 0.062),
        -0.5rem 0 rgba(0, 255, 255, 0.048);
    }
  }
  .middle {
    --c: rgba(0, 0, 0, 1);
    .my-name {
      font-family: "Bungee Shade", sans-serif;
      font-size: clamp(5rem, 5vw, 10rem);
      // font-weight: bold;
      color: rgba(0, 0, 0, 0.4);
    }
    img {
      width: clamp(30rem, 30vw, 40rem);
    }
  }
  .bottom {
    .bottom-left {
      h2 {
        font-size: 2.5rem;
        color: rgb(35, 197, 197);
        font-weight: bold;
        margin-bottom: 1rem;
      }
      p {
        font-size: 1.75rem;
        opacity: 0.7;
      }
    }
    .bottom-right {
      a {
        font-family: "Bungee Shade", sans-serif;
        letter-spacing: 1rem;
        font-size: 2.5rem;
        .my-resume {
          @include flex(row, center, center);
          // overflow: hidden;
          background: rgba(0, 0, 0, 0.2);
          position: relative;
          padding: 2rem;
          width: 11rem;
          height: 11rem;
          border-radius: 50%;
          text-align: center;

          &::after {
            content: "";
            position: absolute;
            z-index: -1;
            border-radius: 50%;
            // border: 0.2rem dashed transparent;
            border: 0.2rem solid transparent;
            border-top-color: rgba(0, 255, 255, 0.793);
            // border-right-color: rgba(0, 255, 255, 0.493);
            border-bottom-color: rgba(0, 255, 255, 0.793);
            inset: 0rem;
            // animation: rotateCW 5s infinite linear;
          }
          @keyframes rotateCW {
            from {
              transform: rotate(0deg);
            }
            to {
              transform: rotate(360deg);
            }
          }
        }
      }
    }
  }
}
</style>
