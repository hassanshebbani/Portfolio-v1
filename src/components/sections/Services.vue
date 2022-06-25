<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
const serviceModals = ref<HTMLDivElement[]>(),
  serviceModalBtns = ref<HTMLSpanElement[]>(),
  serviceModalsClose = ref<HTMLSpanElement[]>();

const myServices: {
  serviceTitle: string;
  icon: string;
  modalList: string[];
}[] = [
  {
    serviceTitle: "UI/UX<br>Designer",
    icon: "uil uil-web-grid",
    modalList: [
      "I develop stunning user interfaces",
      "Landing pages for your product",
      "Interactive user experiences that hooks users",
      "I position your company brand",
    ],
  },
  {
    serviceTitle: "Full Stack<br>Development",
    icon: "uil uil-arrow",
    modalList: [
      "Interactive user experiences that hooks users",
      "I position your company brand",
    ],
  },
  {
    serviceTitle: "Branding",
    icon: "uil uil-pen",
    modalList: [
      "I develop stunning user interfaces and very stunning visuals.",
      "Landing pages for your product",
      "I position your company brand",
    ],
  },
];
const animateServiceModals = () => {
  const serviceModalTimeline: GSAPTimeline = gsap.timeline({
    defaults: {
      duration: 0.75,
      ease: "power2.inOut",
    },
  });
  const totalModals = serviceModalBtns.value!.length;
  for (let i = 0; i < totalModals; i++) {
    serviceModalBtns.value![i].addEventListener("click", () => {
      serviceModalTimeline.to(serviceModals.value![i], {
        clipPath: "circle(100%)",
      });
      serviceModalTimeline.fromTo(
        serviceModals.value![i].children[0],
        { opacity: 0, y: "20%" },
        { duration: 0.5, opacity: 1, y: "0%" }
      );
    });
  }
  for (let i = 0; i < totalModals; i++) {
    serviceModalsClose.value![i].addEventListener("click", () => {
      serviceModalTimeline.to(serviceModals.value![i], {
        duration: 1,
        clipPath: "circle(0%)",
      });
    });
  }
};
onMounted(async () => {
  animateServiceModals();
});
</script>

<template>
  <!-- Services Section -->
  <section class="services-section" id="services">
    <h2>What I Offer</h2>
    <div
      class="services-container grid md:grid-cols-3 lg:grid-cols-3 gap-10 lg:gap-20"
    >
      <div
        v-for="(item, index) in myServices"
        :key="index"
        class="content flex items-center"
      >
        <div class="card" :style="`height:${index % 2 !== 0 ? '45' : '40'}rem`">
          <ul class="ul">
            <li class="text-center animate-pulse">
            </li>
          </ul>
          <div class="con-text">
            <h2 v-html="item.serviceTitle"></h2>
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolorem
              eaque odio mollitia vitae, doloribus repellat fugit tenetur?
            </p>
            <button class="cta activate-cursor" ref="serviceModalBtns">
              See more
            </button>
          </div>
        </div>
        <div class="modal" ref="serviceModals">
          <div class="modal-content">
            <div class="top">
              <h4>{{item.serviceTitle.replace("<br />", " ")}}</h4>
              <i
                class="uil uil-times modal-close activate-cursor"
                ref="serviceModalsClose"
              ></i>
            </div>
            <ul class="modal-services">
              <li
                v-for="(note, index) in item.modalList"
                :key="index"
                class="service"
              >
                <i class="uil uil-check-circle"></i>
                <p>{{ note }}</p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.card {
  border: 0.15rem solid rgba(0, 255, 255, 0.514);
  width: 30rem;
  border-radius: 3rem;
  overflow: hidden;
  position: relative;
  @include flex(row, center, center);
  transition: all 0.45s ease;
  backface-visibility: hidden;
  text-align: left;
  &:hover {
    @include flex(row, center, space-between);
    height: 100%;

    transform: scale(1.05);
    .con-text p,
    .con-text button {
      margin-bottom: 0rem;
      opacity: 1;
      transition: all 0.4s;
    }
    &::after {
      height: 280rem;
    }
    img {
      transform: scale(1.25);
    }
    .ul {
      transform: translate(0);
      opacity: 1;
    }
  }

  &::after {
    width: 100%;
    content: "";
    left: 0rem;
    bottom: 0rem;
    height: 15rem;
    position: absolute;
    background: linear-gradient(
      180deg,
      rgba(0, 0, 0, 0) 0%,
      rgba(0, 0, 0, 0.5) 100%
    );
    z-index: 2;
    transition: all 0.45s ease;
  }
  .ul {
    @include flex(column, center, center);
    position: absolute;
    top: 2rem;
    right: 2rem;
    display: flex;
    z-index: 3;
    padding-bottom: 0.8rem;
    opacity: 0;
    transform: translate(100%);
    transition: all 0.25s ease;
    li {
      @include flex(row, center, center);
      cursor: pointer;
      list-style: none;
      width: 15rem;
      padding: 2rem;
      opacity: 0.9;
      transition: all 0.25s ease;
      backface-visibility: hidden;
      color: white;
      font-size: 1.75rem;
      font-weight: bold;

      &:hover {
        opacity: 1;
        transform: translate(-0.7rem, -0.4rem);
      }
      i {
        font-size: 1.75rem;
        color: #fff;
      }
    }
  }
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: 2;
    transition: all 0.25s ease;
  }
  .con-text {
    z-index: 3;
    position: absolute;
    bottom: 0rem;
    color: #fff;
    padding: 2rem;
    padding-bottom: 3rem;
    @include flex(column, flex-start, flex-end);
    h2 {
      font-size: 3rem;
      font-family: "Poppins", sans-serif;
      text-align: left;
    }
    button {
      opacity: 0;
      align-self: flex-end;
      transition: all 0.4s;
    }
    p {
      opacity: 0;
      font-size: 1.5rem;
      opacity: 0;
      margin-bottom: -15rem;
      transition: all 0.45s ease;
    }
  }
}
.services-section {
  .services-container {
    margin-top: 4rem;
    .content {
      position: relative;
      .leading {
        @include flex(column, center, center);
        text-align: center;
        font-size: 2rem;
        .cta {
          @include flex(row, center, center);
          background: transparent;
          color: rgb(3, 211, 211);
          box-shadow: 0 0.2rem 0.4rem rgba(0, 231, 231, 0.63);
          font-size: 1.5rem;
          font-weight: bold;
          padding: 0.75rem 1.25rem;
          transition: all 0.3s;
          i {
            font-size: 2rem;
            margin-left: 1rem;
          }
          &:hover {
            background: rgb(3, 211, 211);
            color: #fff;
            box-shadow: 0 0.4rem 0.8rem rgba(0, 231, 231, 0.63);
            transform: translateY(-0.5rem);
            transition: all 0.3s;
          }
        }
      }
      .modal {
        @include flex(row, center, center);
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        z-index: 4;
        background: rgba(0, 0, 0, 0.5);
        padding: 0 1rem;
        clip-path: circle(0%);
        backdrop-filter: blur(0.4rem);
        .modal-content {
          color: black;
          opacity: 0;
          position: relative;
          background: white;
          padding: 3rem 2rem;
          border-radius: 0.5rem;
          font-size: 2rem;
          .top {
            @include flex(row, center, space-between);
            h4 {
              font-weight: bold;
            }
            .modal-close {
              font-size: 2.5rem;
              cursor: pointer;
            }
          }
          .modal-services {
            li {
              display: flex;
              margin: 2rem 0;
              font-size: 1.75rem;
              i {
                margin-right: 1rem;
              }
            }
          }
        }
      }
    }
  }
}
</style>
