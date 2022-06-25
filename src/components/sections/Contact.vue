<script setup lang="ts">
import { ref, onMounted } from "vue";
import SocialsVue from "../Socials.vue";
import gsap from "gsap";
const sendMsgBtn = ref<HTMLButtonElement>();
const contactMethods: { method: string; info: string; icon: string }[] = [
  { method: "Phone", info: "+961 76 822 948", icon: "uil uil-phone" },
  { method: "Email", info: "hsmh@gmail.com", icon: "uil uil-envelope" },
  {
    method: "Location",
    info: "Wherever there's a signal <i class='uil uil-wifi'></i>",
    icon: "uil uil-map-marker",
  },
];
const animateSendMsgBtn = () => {
  sendMsgBtn.value!.addEventListener("click", (e: Event) => {
    (e.target as HTMLButtonElement)!.classList.add("loading");

    setTimeout(() => {
      (e.target as HTMLButtonElement)!.classList.remove("loading");
    }, 3000);
  });
};
onMounted(async () => {
  animateSendMsgBtn();
});
</script>

<template>
  <!-- Contact Section -->
  <section class="contact-section" id="contact">
    <h2>Let's Get In Touch!</h2>
    <div class="contact-container flex flex-col lg:grid grid-cols-2 gap-10">
      <div class="contact-methods flex flex-col items-center justify-start">
        <div
          class="flex flex-row lg:flex-col flex-wrap w-full lg:w-fit lg:mb-10"
        >
          <div
            v-for="(item, index) in contactMethods"
            :key="index"
            class="contact-info flex-1 w-full basis-72 lg:basis-0"
          >
            <i :class="item.icon"></i>
            <div class="contact-details">
              <h3>{{ item.method }}</h3>
              <span v-html="item.info"></span>
            </div>
          </div>
        </div>
        <SocialsVue
          class="hidden md:flex md:mt-10"
          :all-class="'flex items-center justify-center'"
          :single-class="'mx-10'"
        />
      </div>
      <form action="" class="contact-form">
        <div class="contact-inputs">
          <div class="flex flex-col xl:grid grid-cols-2 xl:gap-10">
            <div class="content">
              <label for="">Name</label>
              <input type="text" />
            </div>
            <div class="content">
              <label for="">Email</label>
              <input type="email" />
            </div>
          </div>
          <div class="content">
            <label for="">Subject - Project</label>
            <input type="text" />
          </div>
          <div class="content">
            <label for="">Message</label>
            <textarea name="" rows="5"></textarea>
          </div>
          <button
            @click.prevent
            class="send-msg-btn activate-cursor"
            ref="sendMsgBtn"
          >
            <i class="uil uil-telegram-alt"></i>
            <span class="text"> Send Message </span>
            <span class="loading-animate"></span>
          </button>
        </div>
      </form>
      <SocialsVue
        :all-class="'flex items-center justify-center'"
        class="flex md:hidden self-center mt-10"
        :single-class="'mx-10'"
      />
    </div>
  </section>
</template>

<style lang="scss" scoped>
.contact-section {
  .contact-container {
    width: 100%;
    margin: 3rem 0;
    .contact-methods {
      .contact-info {
        @include flex(row, center, auto);
        justify-self: center;
        margin-bottom: 3rem;
        h3 {
          font-size: clamp($small-sub-fs, 2vw, $medium-sub-fs);
        }
        span {
          font-size: clamp($medium-sub-fs, 2vw, $medium-fs);

          opacity: 0.9;
        }
        i {
          font-size: 3rem;
          color: rgb(0, 199, 199);
          margin-right: 1.5rem;
        }
      }
    }
    .contact-form {
      width: 100%;
      .contact-inputs {
        .content {
          @include flex(column, flex-start, space-between);
          margin-bottom: 2rem;
          label {
            font-size: 1.75rem;
            margin-bottom: 1.25rem;
          }
          input,
          textarea {
            font-size: clamp($medium-sub-fs, 2vw, $medium-fs);
            width: 100%;
            border: none;
            outline: none;
            border-bottom: 0.1rem solid rgba(0, 255, 255, 0.8);
            resize: none;
            padding: 1rem 1.75rem;
            border-radius: 0.5rem;
            background: rgba(0, 212, 212, 0.219);
          }
        }

        .send-msg-btn {
          @include flex(row, center, center);
          margin-left: auto;
          justify-self: flex-end;
          background: #01969b;
          border: 0 solid #07ebfc;
          border-radius: 3.5rem;
          font-size: 1.75rem;
          color: #fff;
          outline: none;
          transition: all 0.3s ease;
          width: 20rem;
          height: 5rem;
          position: relative;
          overflow: hidden;
          // margin-bottom: -2rem;
          transform: translateY(2rem);
          &:hover {
            transform: translateY(-0.5rem);
            transition: all 0.3s ease;
          }
          &:not(.loading):hover {
            box-shadow: 0 0.1rem 2.5rem 0 rgba(73, 215, 215, 0.8);
          }
          &:not(.loading):hover i {
            transform: translate(1rem);
          }
          i {
            @include flex(row, center, center);
            position: absolute;
            left: 0;
            pointer-events: none;
            z-index: 3;
            background: inherit;
            width: 5rem;
            height: 5rem;
            border-radius: 50%;
            transition: all 0.3s ease;
          }
          .text {
            display: block;
            font-size: 1.6rem;
            width: 100%;
            margin-left: 4rem;
            pointer-events: none;
            transition: all 0.3s ease;
          }
          .loading-animate {
            @include flex(row, center, center);
            position: absolute;
            top: 0;
            left: 0;
            width: 5rem;
            height: 5rem;
            z-index: 3;
            border-radius: 50%;
            pointer-events: none;
            opacity: 0;
            transition: all 0.3s ease;
            &:after {
              content: "";
              width: 4.4rem;
              height: 4.4rem;
              border-radius: 50%;
              border: 0.3rem solid transparent;
              border-top: 0.3rem solid #fff;
              position: absolute;
              animation: loading infinite 0.8s ease 0.05s;
            }
            @keyframes loading {
              0% {
                transform: rotate(0deg);
              }
              100% {
                transform: rotate(360deg);
              }
            }
          }
          &.loading {
            width: 5rem;
            i {
              transform: rotate(-90deg);
              padding-bottom: 0.4rem;
              padding-left: 0.3rem;
            }
            &.text {
              transform: translate(-15rem);
            }
          }
          &.loading .loading-animate {
            opacity: 1;
          }
        }
      }
    }
  }
}
</style>
