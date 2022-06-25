<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
// Swiper
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/effect-creative";
import "swiper/css/autoplay";
import "swiper/css/scrollbar";
import { EffectCreative, Pagination, Autoplay, Scrollbar } from "swiper";
import "swiper/css/pagination";
import SocialsVue from "../components/Socials.vue";
const modules = [EffectCreative, Pagination, Autoplay, Scrollbar];
const skillArrows = ref<HTMLDivElement[]>(),
  eduTab = ref<HTMLDivElement>(),
  workTab = ref<HTMLDivElement>(),
  qualContent = ref<HTMLDivElement>(),
  qualSection = ref<HTMLDivElement>(),
  serviceModals = ref<HTMLDivElement[]>(),
  serviceModalBtns = ref<HTMLSpanElement[]>(),
  serviceModalsClose = ref<HTMLSpanElement[]>(),
  sendMsgBtn = ref<HTMLButtonElement>();
const skills: {
  heading: string;
  duration: string;
  icon: string;
  skillset: { skill: string; percentage: string }[];
}[] = [
  {
    heading: "Frontend Development",
    duration: "More than 4 years",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "Vue Js", percentage: "100" },
      { skill: "Three Js", percentage: "60" },
      { skill: "Tailwind CSS", percentage: "100" },
      { skill: "Bootstrap CSS", percentage: "100" },
      { skill: "GSAP", percentage: "40" },
    ],
  },
  {
    heading: "Backend Development",
    duration: "More than 5 years",
    icon: "uil uil-server-network",
    skillset: [
      { skill: "Node Js", percentage: "100" },
      { skill: "Nuxt Js", percentage: "40" },
    ],
  },
  {
    heading: "Mobile Development",
    duration: "More than 5 years",
    icon: "uil uil-swatchbook",
    skillset: [
      { skill: "Flutter", percentage: "50" },
      { skill: "Java", percentage: "30" },
    ],
  },
  {
    heading: "Databases & DBMS",
    duration: "More than 5 years",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "MongoDB", percentage: "60" },
      { skill: "MySQL", percentage: "60" },
      { skill: "SQLite", percentage: "70" },
    ],
  },
  {
    heading: "User Interface & Experience Design",
    duration: "More than 5 years",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "Figma", percentage: "100" },
      { skill: "Adobe Photoshop", percentage: "60" },
      { skill: "Adobe Illustrator", percentage: "50" },
    ],
  },
  {
    heading: "Miscellaneous",
    duration: "More than 5 years",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "Progressive Web Apps PWA", percentage: "20" },
      { skill: "Python", percentage: "60" },
      { skill: "Rust", percentage: "20" },
    ],
  },
];
interface Qualification {
  heading: string;
  subHeading: string;
  dates: string;
  icon: string;
}
const qualEdu: Qualification[] = [
  {
    heading: "Computer Scientist",
    subHeading: "Lebanese International University",
    dates: "2019 - 2022",
    icon: "",
  },
  {
    heading: "Computer Scientist",
    subHeading: "Lebanese International University",
    dates: "2019 - 2022",
    icon: "",
  },
  {
    heading: "SAT 1100/1600",
    subHeading: "Amideast",
    dates: "2016",
    icon: "",
  },
  {
    heading: "SAT 1100/1600",
    subHeading: "Amideast",
    dates: "2016",
    icon: "",
  },
  {
    heading: "SAT 1100/1600",
    subHeading: "Amideast",
    dates: "2016",
    icon: "",
  },
];
const qualWork: Qualification[] = [
  {
    heading: "Work Scientist",
    subHeading: "Lebanese International University",
    dates: "2019 - 2022",
    icon: "",
  },
  {
    heading: "Work",
    subHeading: "Amideast - Lebanon",
    dates: "2016",
    icon: "",
  },
  {
    heading: "Work Scientist",
    subHeading: "Lebanese International University",
    dates: "2019 - 2022",
    icon: "",
  },
];
const toShowQual = ref<Qualification[]>(qualEdu);
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
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur ullam, a, alias ea at possimus reprehenderit, assumenda modi aperiam nihil fugiat vitae sapiente. Exercitationem reiciendis id modi omnis temporibus fugiat!",
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
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut maxime eveniet deserunt cumque sit animi nihil nobis possimus nemo, ut harum, quisquam, nam rerum modi magni. Asperiores fugiat soluta quas!",
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
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut maxime eveniet deserunt cumque sit animi nihil nobis possimus nemo, ut harum, quisquam, nam rerum modi magni. Asperiores fugiat soluta quas!",
  },
  {
    clientName: "Jomaica Brunoz",
    clientPosition: "Talent Recruiter",
    clientImg: "t4.jpg",
    stars: 4,
    testimony: "Lorem ipsum dolor sit amet consectetur adipisicing elit!",
  },
];
const contactMethods: { method: string; info: string; icon: string }[] = [
  { method: "Phone", info: "+961 76 822 948", icon: "uil uil-phone" },
  { method: "Email", info: "hsmh@gmail.com", icon: "uil uil-envelope" },
  {
    method: "Location",
    info: "Wherever there's a signal <i class='uil uil-wifi'></i>",
    icon: "uil uil-map-marker",
  },
];
const animateSkills = () => {
  for (let i = 0; i < skillArrows.value!.length; i++) {
    skillArrows.value![i].addEventListener("click", (e: Event) => {
      const arrow = e.target! as HTMLDivElement;
      const skillsList = arrow.parentElement?.parentElement?.querySelectorAll(
        ".skills-list"
      )! as NodeList;
      //   const skillSets = arrow.parentElement?.parentElement?.querySelectorAll(
      //     ".skillset"
      //   )! as NodeList;
      const skillDetails = arrow.parentElement?.parentElement?.querySelectorAll(
        ".skillset .skill-details"
      )! as NodeList;
      const skillPBs = arrow.parentElement?.parentElement?.querySelectorAll(
        ".skillset .skill-progress-bar"
      )! as NodeList;
      const skillsTimeline: GSAPTimeline = gsap.timeline({
        defaults: {
          duration: 1,
          ease: "power2.inOut",
        },
      });
      if (!arrow.classList.contains("opened")) {
        gsap.to(skillArrows.value![i], {
          duration: 2,
          rotateX: "180deg",
          rotateY: "360deg",
          ease: "power2.inOut",
        });
        skillsTimeline.to(skillsList, {
          duration: 0.75,
          opacity: 1,
          height: "auto",
          overflow: "visible",
        });
        skillsTimeline.fromTo(
          skillDetails,
          { duration: 0.75, opacity: 0, x: "-20%" },
          { duration: 0.75, opacity: 1, x: "0%" }
        );
        skillsTimeline.fromTo(
          skillPBs,
          { duration: 0.75, opacity: 0, width: "0%" },
          { duration: 0.75, opacity: 1, width: "100%" },
          "-=0.15"
        );
      } else {
        gsap.to(skillArrows.value![i], {
          duration: 2,
          rotateX: "0deg",
          ease: "power2.inOut",
        });
        skillsTimeline.to(
          skillPBs,
          { duration: 0.75, opacity: 0, width: "0%" },
          "-=0.15"
        );
        skillsTimeline.to(skillsList, {
          duration: 0.75,
          opacity: 0,
          height: "0",
          overflow: "hidden",
        });
        skillsTimeline.to(skillDetails, {
          duration: 0.75,
          opacity: 0,
          x: "-20%",
        });
      }
      arrow.classList.toggle("opened");
    });
  }
};
const switchQualTabs = async (switchToTab: string) => {
  const qualTimeline: GSAPTimeline = gsap.timeline({
    defaults: {
      duration: 1,
      ease: "power2.inOut",
    },
  });
  //   await qualTimeline.to(qualSection.value!, {height: 0})
  if (switchToTab === "Education") {
    await qualTimeline.to(qualContent.value!, {
      opacity: 0,
      x: "100%",
    });
    toShowQual.value = qualEdu;
    qualTimeline.fromTo(
      qualContent.value!,
      {
        opacity: 0,
        x: "-100%",
      },
      {
        opacity: 1,
        x: "0%",
      }
    );
  } else {
    await qualTimeline.to(qualContent.value!, {
      opacity: 0,
      x: "-100%",
    });
    toShowQual.value = qualWork;
    qualTimeline.fromTo(
      qualContent.value!,
      {
        opacity: 0,
        x: "100%",
      },
      {
        opacity: 1,
        x: "0%",
      }
    );
  }
  // qualTimeline.to(qualSection.value!, {height: "fit-content"})
};
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
const animateSendMsgBtn = () => {
  sendMsgBtn.value!.addEventListener("click", (e: Event) => {
    (e.target as HTMLButtonElement)!.classList.add("loading");

    setTimeout(() => {
      (e.target as HTMLButtonElement)!.classList.remove("loading");
    }, 3000);
  });
};
onMounted(async () => {
  animateSkills();
  eduTab.value!.addEventListener("click", () => switchQualTabs("Education"));
  workTab.value!.addEventListener("click", () => switchQualTabs("Work"));
  animateServiceModals();
  animateSendMsgBtn();
  window.addEventListener("scroll", activateNavSections);
});
</script>

<template>
  <main class="main">
    <!-- Home Section -->
    <section class="home-section" id="home">
      <div class="home-container container grid">
        <div class="content grid">
          <!-- <div class="socials">
                    <a to="#"></a>
                </div> -->
          <SocialsVue />
          <img src="/favicon.ico" alt="" />
          <div class="leading">
            <h1>Hi, I am Hassan</h1>
            <h3>Full Stack Web & Mobile Developer</h3>
            <p>
              Lorem ipsum dolor sit amet consectetur, adipisicing elit. Velit,
              numquam vel voluptatibus error expedita corporis at, voluptatum
              corrupti autem.
            </p>
            <a to="#contact" class="cta"
              ><span>Contact Me</span><i class="uil uil-message"></i
            ></a>
          </div>
        </div>
        <!-- <div class="scroll">
          <a to="#about">
            <i class="uil uil-mouse-alt"></i> <span>Scroll down</span
            ><i class="uil uil-arrow-down"></i>
          </a>
        </div> -->
      </div>
    </section>
    <br />
    <!-- About Section -->
    <section class="about-section" id="about">
      <h2>About Me</h2>
      <br />
      <div class="about-container container grid">
        <img src="/favicon.ico" alt="" />
        <br />
        <div class="leading">
          <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Corrupti
            voluptas quos, eos animi quod sapiente neque, delectus rerum aut at
            minima vel adipisci.
          </p>
          <br />
          <div class="about-info">
            <div class="info">
              <p>08+</p>
              <span
                >Years <br />
                experience</span
              >
            </div>
            <div class="info">
              <p>20+</p>
              <span
                >Completed <br />
                projects</span
              >
            </div>
            <div class="info">
              <p>05+</p>
              <span
                >Companies <br />
                worked</span
              >
            </div>
          </div>
          <a
            class="resume w-fit"
            download
            target="_blank"
            href="/sample-pdf.pdf"
          >
            <span>Resume</span><i class="uil uil-download-alt"></i>
          </a>
        </div>
      </div>
    </section>
    <br />
    <!-- Skills Section -->
    <section class="skills-section" id="skills">
      <h2>Skills</h2>
      <div class="skills-container">
        <div
          class="all-skills grid xl:grid-cols-3 gap-0 xl:gap-x-20 xl:gap-y-10"
        >
          <div v-for="(item, index) in skills" :key="index" class="skill">
            <div class="heading grid grid-cols-6 items-center justify-center">
              <i class="col-span-1" :class="item.icon"></i>
              <div class="col-span-4">
                <h1>{{ item.heading }}</h1>
                <span>{{ item.duration }}</span>
              </div>
              <i
                class="uil uil-angle-down col-span-1 justify-self-end"
                ref="skillArrows"
              ></i>
            </div>
            <!-- Skill set -->
            <div
              v-for="(skill, index) in item.skillset"
              :key="index"
              class="skills-list grid"
            >
              <div>
                <div class="skillset">
                  <div class="skill-details">
                    <span>{{ skill.skill }}</span>
                    <span>{{ skill.percentage + "%" }}</span>
                  </div>
                  <div
                    class="skill-progress-bar"
                    :style="`--percentage: ${skill.percentage}%;`"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <br />
    <!-- Qualifications Section -->
    <section class="qualifications-section">
      <h2>My Personal Journey</h2>
      <div class="qualifications-container">
        <div class="tabs">
          <div class="education-tab active" ref="eduTab">
            <i class="uil uil-graduation-cap"></i><span>Education</span>
          </div>
          <div class="work-tab" ref="workTab">
            <i class="uil uil-briefcase-alt"></i><span>Work</span>
          </div>
        </div>
        <div class="sections" ref="qualSection">
          <div class="content" ref="qualContent">
            <div
              v-for="(item, index) in toShowQual"
              :key="index"
              class="leading"
            >
              <div v-if="index % 2 !== 0"></div>
              <div v-if="index % 2 !== 0">
                <span class="rounder"></span>
                <span class="line"></span>
              </div>
              <div>
                <h3>{{ item.heading }}</h3>
                <span class="sub-heading">{{ item.subHeading }}</span>
                <div class="dates">
                  <i class="uil uil-calendar-alt"></i>
                  <span class="dates">{{ item.dates }}</span>
                </div>
              </div>
              <div v-if="index % 2 === 0">
                <span class="rounder"></span>
                <span
                  v-if="!(index === toShowQual.length - 1)"
                  class="line"
                ></span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Services Section -->
    <section class="services-section" id="services">
      <h2>What I Offer</h2>
      <div
        class="services-container grid md:grid-cols-3 lg:grid-cols-3 gap-10 lg:gap-20"
      >
        <div v-for="(item, index) in myServices" :key="index" class="content">
          <div class="leading">
            <i :class="item.icon"> </i>
            <h3 v-html="item.serviceTitle"></h3>
            <span class="cta" ref="serviceModalBtns">
              View more
              <i class="uil uil-arrow-right"></i>
            </span>
          </div>
          <div class="modal" ref="serviceModals">
            <div class="modal-content">
              <div class="top">
                <h4>{{item.serviceTitle.replace("<br />", " ")}}</h4>
                <i
                  class="uil uil-times modal-close"
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
    <!-- Portfolio Section -->
    <section class="portfolio-section" id="portfolio">
      <div class="heading">
        <h2 class="">Some of my recent work</h2>
        <div class="hint">
          <span>Swipe</span><i class="uil uil-forward"></i>
        </div>
      </div>
      <div class="portfolio-container">
        <!-- <div> -->
        <swiper
          :grabCursor="true"
          :effect="'creative'"
          :autoplay="{
            delay: 5000,
            disableOnInteraction: false,
            pauseOnMouseEnter: true,
          }"
          :pagination="{
            clickable: true,
            horizontalClass: 'swiper-pagination-horizontal',
            type: 'bullets',
          }"
          :creativeEffect="{
            prev: {
              shadow: false,
              translate: ['-120%', 0, -500],
            },
            next: {
              shadow: false,
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
              <a class="cta" :href="item.link" target="_blank"
                >Demo <i class="uil uil-arrow-right"></i
              ></a>
            </div>
          </swiper-slide>
        </swiper>
      </div>
      <!-- </div> -->
    </section>
    <!-- Testimonials Section -->
    <section class="testimonials-section">
      <h2>What Do My Clients Say?</h2>
      <div class="testimonials-container">
        <swiper
          :scrollbar="{
            // snapOnRelease: true,
            verticalClass: 'swiper-scrollbar-vertical',
          }"
          :autoplay="{
            disableOnInteraction: false,
            pauseOnMouseEnter: true,
            // reverseDirection: true,
          }"
          :breakpoints="{
            568: {
              slidesPerView: 2,
            },
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
            <div class="leading md:px-8">
              <div class="header">
                <img
                  :src="`/assets/images/testimonials/${item.clientImg}`"
                  :alt="item.clientName"
                />
                <div class="header-details">
                  <h3>{{ item.clientName }}</h3>
                  <span>{{ item.clientPosition }}</span>
                </div>
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
              <p>{{ item.testimony }}</p>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </section>
    <!-- Contact Section -->
    <section class="contact-section" id="contact">
      <h2>Let's Get In Touch!</h2>
      <div class="contact-container">
        <div class="contact-methods">
          <div
            v-for="(item, index) in contactMethods"
            :key="index"
            class="contact-info"
          >
            <i :class="item.icon"></i>
            <div class="contact-details">
              <h3>{{ item.method }}</h3>
              <span v-html="item.info"></span>
            </div>
          </div>
        </div>
        <form action="" class="contact-form">
          <div class="contact-inputs">
            <div class="content">
              <label for="">Name</label>
              <input type="text" />
            </div>
            <div class="content">
              <label for="">Email</label>
              <input type="email" />
            </div>
            <div class="content">
              <label for="">Project</label>
              <input type="text" />
            </div>
            <div class="content">
              <label for="">Message</label>
              <textarea name="" rows="5"></textarea>
            </div>
            <button @click.prevent class="send-msg-btn" ref="sendMsgBtn">
              <i class="uil uil-telegram-alt"></i>
              <span class="text"> Send Message </span>
              <span class="loading-animate"></span>
            </button>
          </div>
        </form>
      </div>
    </section>
    <!-- <br> -->
    <!-- <hr class="my-60"> -->
  </main>
</template>

<style lang="scss" scoped>
@mixin flex($direction, $align, $justify) {
  display: flex;
  flex-direction: $direction;
  align-items: $align;
  justify-content: $justify;
}
.send-msg-btn {
  @include flex(row, center, center);
  margin-left: auto;
  justify-self: flex-end;
  background: #49d2d7;
  border: 0 solid #07ebfc;
  border-radius: 3.5rem;
  font-size: 1.75rem;
  color: #fff;
  cursor: pointer;
  outline: none;
  transition: all 0.3s ease;
  width: 20rem;
  height: 5rem;
  position: relative;
  overflow: hidden;
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

.home-section,
.about-section,
.skills-section,
.qualifications-section,
.services-section,
.portfolio-section,
.testimonials-section,
.contact-section {
  margin-bottom: 1rem;
  // background: rgba(0, 0, 0, 0.3);
  @include flex(column, center, center);
  width: 100%;
  padding: 2rem;
  @media screen and (min-width: 767px) {
    width: 80%;
    margin: auto;
  }
  h2 {
    font-size: 2rem;
    font-weight: bold;
  }
}

.home-section {
  .home-container {
    gap: 1rem;
    .content {
      grid-template-columns: 0.5fr 3fr;
      align-items: center;
      img {
        width: 25rem;
        // height: 25rem;
        justify-self: center;
        align-self: center;
      }
    }
    .leading {
      grid-column: 1/3;
      h1 {
        font-size: 3rem;
        font-weight: bold;
      }
      h3 {
        font-size: 2rem;
      }
      p {
        font-size: 1.5rem;
        margin-bottom: 2rem;
      }
    }
    // .scroll {
    //     transform: all 0.3s;
    //     &:hover {
    //         transform: scale(1.2);
    //         transition: all 0.3s;
    //     }
    // }
  }
}

.about-section {
  .about-container {
    img {
      width: 25rem;
      border-radius: 1rem;
      justify-self: center;
      align-self: center;
    }
    .leading {
      @include flex(column, center, space-between);
      p {
        text-align: center;
        font-size: 1.5rem;
      }
      .about-info {
        @include flex(row, center, space-between);
        width: 80%;
        .info {
          text-align: center;
          p {
            font-size: 2.5rem;
            font-weight: bold;
          }
        }
      }
    }
  }
}

.skills-section {
  .skills-container {
    .all-skills {
      .skill {
        margin: 1.5rem 0;
        .heading {
          i {
            font-size: 3rem;
          }
          h1 {
            font-size: 1.75rem;
            font-weight: bold;
          }
          span {
            font-size: 1.25rem;
            opacity: 0.8;
          }
        }
        .skills-list {
          height: 0;
          overflow: hidden;
          .skillset {
            padding: 0 4rem;
            margin: 1rem 0;
            .skill-details {
              @include flex(row, center, space-between);
              font-size: 1.5rem;
              font-weight: bold;
              margin-bottom: 1rem;
              opacity: 0;
              span {
                &:last-child {
                  font-weight: 400;
                }
              }
            }
            .skill-progress-bar {
              opacity: 0;
              position: relative;
              height: 0.75rem;
              &::before,
              &::after {
                content: "";
                position: absolute;
                top: 0;
                left: 0;
                height: 100%;
                width: 100%;
                background: rgba(0, 0, 0, 0.164);
                //   border-radius: 0 1rem 1rem 0;
                border-radius: 1rem;
              }
              &::after {
                background: rgb(5, 197, 255);
                width: var(--percentage);
              }
            }
          }
        }
      }
    }
  }
}

.qualifications-section {
  overflow: hidden;
  .qualifications-container {
    .tabs {
      @include flex(row, center, space-around);
      font-size: 2rem;
      margin: 2rem 0rem;
      .education-tab,
      .work-tab {
        cursor: pointer;
        opacity: 0.7;
        i {
          margin-right: 1rem;
        }
      }
      .active {
        opacity: 1;
        color: cyan;
      }
    }
    .sections {
      padding: 2rem 0;
      .content {
        .leading {
          display: grid;
          grid-template-columns: 1fr max-content 1fr;
          column-gap: 1.5rem;
          i {
            margin-right: 1.5rem;
          }
          h3 {
            font-size: 2rem;
            font-weight: bold;
          }
          .sub-heading {
            font-size: 1.75rem;
          }
          .dates {
            font-size: 1.5rem;
            opacity: 0.8;
            margin-top: 1.5rem;
          }
          .rounder {
            display: inline-block;
            width: 1.3rem;
            height: 1.3rem;
            background: cyan;
            border-radius: 50%;
            position: relative;
            z-index: 2;
          }
          .line {
            display: block;
            opacity: 0.2;
            width: 0.2rem;
            height: 100%;
            background: black;
            transform: translate(0.55rem, -0.7rem);
          }
        }
      }
    }
  }
}

.services-section {
  justify-content: space-between;
  .services-container {
    margin-top: 4rem;
    .content {
      position: relative;
      // background: linear-gradient(to bottom, rgba(243, 205, 147, 0.616), rgba(0, 255, 255, 0.288));
      // color: white;
      background: rgb(245, 245, 245);
      padding: 3rem 2rem;
      border-radius: 0.25rem;
      box-shadow: 0 0.2rem 0.4rem rgba(0, 247, 255, 0.349);
      transition: all 0.3s;
      &:hover {
        box-shadow: 0 0.8rem 1rem rgba(0, 247, 255, 0.349);
        transition: all 0.3s;
      }
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
        z-index: 2;
        background: rgba(0, 0, 0, 0.5);
        padding: 0 1rem;
        clip-path: circle(0%);
        backdrop-filter: blur(0.4rem);
        .modal-content {
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

.portfolio-section {
  .heading {
    @include flex(row, center, center);
    width: 100%;
    h2 {
      margin-left: auto;
      justify-self: center;
    }
    .hint {
      @include flex(row, center, center);
      margin-left: auto;
      justify-self: flex-end;
      font-size: 1.5rem;
      opacity: 0.7;
      span {
        margin-right: 1rem;
      }
    }
  }
  .portfolio-container {
    overflow: initial;
    margin-top: 3rem;

    .content {
      margin-bottom: 5rem;
      img {
        border-radius: 1.5rem;
        box-shadow: 0 0.8rem 1rem rgba(0, 0, 0, 0.2);
        justify-self: center;
      }
      .leading {
        @include flex(column, flex-start, flex-start);
        h3 {
          font-size: 1.75rem;
          font-weight: bold;
          // top horizontal bottom
          margin: 2rem 0 1rem;
        }
        p {
          font-size: 1.5rem;
          font-weight: 400;
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

.testimonials-section {
  .testimonials-container {
    margin-top: 3rem;
    .content {
      @include flex(column, center, center);
      .leading {
        @include flex(column, flex-start, flex-start);
        .header {
          @include flex(row, flex-start, auto);
          width: 100%;
          img {
            width: 6rem;
            height: 6rem;
            border-radius: 50%;
            margin-right: 1.75rem;
            object-fit: contain;
          }
          .header-details {
            h3 {
              font-size: 1.75rem;
              font-weight: bold;
            }
            span {
              font-size: 1.5rem;
              color: rgb(1, 207, 207);
              font-weight: bold;
              // opacity: 0.7;
            }
          }
          .stars {
            justify-self: flex-end;
            @include flex(row, center, center);
            margin-left: auto;
            color: rgb(0, 199, 199);
            font-size: 1.5rem;
          }
        }
        p {
          font-size: 1.5rem;
          padding-left: 7.75rem;
          opacity: 0.85;
        }
      }
    }
  }
}

.contact-section {
  .contact-container {
    @media screen and (max-width: 767px) {
      @include flex(column, center, center);
      width: 100%;
    }
    width: 100%;
    margin: 3rem 0;
    .contact-methods {
      @include flex(row, flex-start, space-between);
      @media screen and (max-width: 767px) {
        @include flex(column, flex-start, center);
      }
      .contact-info {
        @include flex(row, center, auto);
        justify-self: center;
        margin-bottom: 3rem;
        h3 {
          font-size: 1.75rem;
        }
        span {
          font-size: 1.5rem;
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
            margin-bottom: 1rem;
          }
          input,
          textarea {
            font-size: 1.5rem;
            width: 100%;
            border: none;
            outline: none;
            resize: none;
            padding: 1rem 1.75rem;
            border-radius: 0.25rem;
            background: rgba(0, 212, 212, 0.219);
          }
        }
      }
    }
  }
}

.swiper-portfolio {
  width: clamp(10rem, 80vw, 78rem);
  height: fit-content;
}

.swiper-slide-portfolio {
  @include flex(column, center, center);
  padding: 0 1rem 2rem;
}
.swiper-testimonials {
  width: clamp(10rem, 80vw, 78rem);
  background: white;
}

.swiper-slide-testimonials {
  background: white;
  padding: 0 1rem 4rem;
}

.cta,
.resume {
  cursor: pointer;
  font-size: 1.5rem;
  padding: 1rem 1.5rem;
  margin-top: 2rem;
  background: rgb(2, 184, 184);
  border-radius: 1rem;
  text-align: center;
  color: white;
  //   filter: drop-shadow(0 0.4rem 0.8rem cyan);
  box-shadow: 0 1rem 2rem rgba(0, 255, 255, 0.5);
  //   align-self: flex-start;
  span {
    margin-right: 2rem;
  }
}
</style>
