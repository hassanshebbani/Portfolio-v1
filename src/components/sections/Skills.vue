<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
const skillArrows = ref<HTMLDivElement[]>();
const skills: {
  heading: string;
  duration: string;
  icon: string;
  skillset: { skill: string; percentage: string }[];
}[] = [
  {
    heading: "Frontend Development",
    duration: "More than 1 year",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "Vue 3", percentage: "100" },
      // { skill: "Three Js", percentage: "60" },
      { skill: "SASS", percentage: "100" },
      { skill: "Tailwind", percentage: "100" },
      { skill: "Bootstrap", percentage: "100" },
      // { skill: "GSAP", percentage: "80" },
    ],
  },
  {
    heading: "Backend Development",
    duration: "More than 1 year",
    icon: "uil uil-server-network",
    skillset: [
      { skill: "Node Js", percentage: "100" },
      { skill: "Nuxt 3", percentage: "100" },
    ],
  },
  {
    heading: "Android Development",
    duration: "More than 6 months",
    icon: "uil uil-swatchbook",
    skillset: [
      { skill: "Flutter 3 & Dart", percentage: "80" },
      { skill: "Java", percentage: "60" },
    ],
  },
  {
    heading: "Databases & DBMS",
    duration: "More than 1 year",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "NoSQL: &nbsp; &nbsp; MongoDB", percentage: "80" },
      { skill: "SQL: &nbsp; &nbsp; MySQL", percentage: "80" },
    ],
  },
  {
    heading: "UI & UX Design",
    duration: "More than 1 year",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "Figma", percentage: "100" },
      { skill: "Adobe Photoshop", percentage: "60" },
      { skill: "Adobe Illustrator", percentage: "60" },
    ],
  },
  {
    heading: "Miscellaneous",
    duration: "More than 3 months",
    icon: "uil uil-brackets-curly",
    skillset: [
      { skill: "TypeScript", percentage: "100" },
      { skill: "Progressive Web Apps", percentage: "40" },
      { skill: "Python", percentage: "85" },
      { skill: "Rust", percentage: "20" },
    ],
  },
];
const skillContainer = ref<HTMLDivElement>()
const skillsSection = ref<HTMLDivElement>()

const scrollWin = () => {
  skillContainer.value!.scrollTo(0, 200);
}

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

onMounted(async () => {
  animateSkills();

});
</script>

<template>
  <!-- Skills Section -->
  <section class="skills-section" id="skills" ref="skillsSection">
    <h2>Skills</h2>
    <div class="skills-container" ref="skillContainer">
      <div
        v-for="(item, index) in skills"
        :key="index"
        class="all-skills grid md:grid-cols-2 gap-0 xl:gap-x-40 xl:gap-y-10"
      >
        <div class="misc-left hidden md:flex items-center justify-center" v-if="index % 2 === 0">
          <!-- <div class="circle"></div> -->
          <!-- <div class="line"></div> -->
        </div>
        <div
          class="skill"
          
        >
          <div class="heading grid grid-cols-6 items-center justify-center">
            <i class="col-span-1" :class="item.icon"></i>
            <div class="col-span-4 xl:px-10">
              <h1>{{ item.heading }}</h1>
              <span>{{ item.duration }}</span>
            </div>
            <i
              class="uil uil-angle-down col-span-1 justify-self-end activate-cursor"
              @click="scrollWin"
              ref="skillArrows"
            ></i>
          </div>
          <!-- Skill set -->
          <div
            v-for="(skill, index) in item.skillset"
            :key="index"
            class="skills-list grid"
          >
              <div class="skillset">
                <div class="skill-details">
                  <span v-html="skill.skill"></span>
                  <span>{{ skill.percentage + "%" }}</span>
                </div>
                <div
                  class="skill-progress-bar"
                  :style="`--percentage: ${skill.percentage}%;`"
                ></div>
              </div>
          </div>
        </div>
        <div class="misc-right hidden md:flex items-center justify-center" v-if="index % 2 !== 0">
          <!-- <div class="line"></div> -->
          <!-- <div class="circle"></div> -->
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.skills-section {
  .skills-container {
    .all-skills {
      .misc-left,
      .misc-right {
        .circle {
          width: 4rem;
          height: 4rem;
          border-radius: 50%;
          background: rgba(0, 255, 255, 0.5);
        }
        .line {
          width: 10rem;
          height: 0.25rem;
          background: black;
        }
      }

      .skill {
        padding: 2rem;
        border-radius: 1.5rem;
        background: rgba(0, 0, 0, 0.2);
        height: fit-content;
        margin: 1.5rem 0;
        .heading {
          i {
            font-size: 3rem;
          }
          h1 {
            color: rgb(26, 207, 26);
            font-size: clamp($medium-sub-fs, 2vw, $big-sub-fs);
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
              font-size: clamp($small-sub-fs, 2vw, $medium-sub-fs);
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
</style>
