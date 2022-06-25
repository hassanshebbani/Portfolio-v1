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
  <section class="skills-section h-screen" id="skills">
    <h2>Skills</h2>
    <div class="skills-container w-full">
      <div
       
        class="all-skills w-full flex flex-col relative"
      >
        <div v-for="(item, index) in skills"
        :key="index" class="skill absolute" :class="[index % 2 === 0 ? 'self-start': 'self-end', 'bg-red-500']" :style="`top: ${index * 12.5}rem`">
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
</template>


<style lang="scss" scoped>
@mixin flex($direction, $align, $justify) {
  display: flex;
  flex-direction: $direction;
  align-items: $align;
  justify-content: $justify;
}

.skills-section {
  @include flex(column, flex-start, flex-start);
  .skills-container {
    .all-skills {
      .skill {
        // background: red;
        padding: 2rem;
        border-radius: 0.75rem;
        box-shadow: 0 0.8rem 2rem rgba(2, 218, 218, 0.603);
        height: fit-content;
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
</style>
