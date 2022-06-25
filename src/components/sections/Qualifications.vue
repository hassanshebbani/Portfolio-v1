<script setup lang="ts">
import { ref, onMounted } from "vue";
import gsap from "gsap";
const eduTab = ref<HTMLDivElement>(),
  workTab = ref<HTMLDivElement>(),
  qualContent = ref<HTMLDivElement>(),
  qualSection = ref<HTMLDivElement>();
interface Qualification {
  heading: string;
  subHeading: string;
  note: string;
  dates: string;
  icon: string;
}
const qualEdu: Qualification[] = [
  {
    heading: "Masters in Software Engineering",
    subHeading: "Lebanese National University",
    dates: "2022 - 2024",
    note: "Ongoing :)",
    icon: "",
  },
  {
    heading: "Bachelor in Computer Sciences",
    subHeading: "Lebanese International University",
    dates: "2019 - 2022",
    note: "Proud Grad with 3.7 GPA",
    icon: "",
  },
  {
    heading: "SAT - Scholastic Aptitude Test ",
    subHeading: "Amideast",
    note: "Top scorers of 1100/1600",
    dates: "2016",
    icon: "",
  },
];
const qualWork: Qualification[] = [
  {
    heading: "Software Engineer",
    subHeading: "Internship at Murex Global",
    note: "Hopefully :D",
    dates: "2022 - 2022",
    icon: "",
  },
  {
    heading: "Software Developer",
    subHeading: "Global Freelancing",
    note: "Freelancing helping clients globally reach their quotas & goals!",
    dates: "2021 - Eternity",
    icon: "",
  },
  {
    heading: "UI/UX Designer",
    subHeading: "Global Freelancing",
    note: "Freelancing taking on clients globally",
    dates: "2021 - Eternity",
    icon: "",
  },
];
const switchQualTabs = async (switchToTab: string) => {
  const qualTimeline: GSAPTimeline = gsap.timeline({
    defaults: {
      duration: 1,
      ease: "power2.inOut",
    },
  });
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
    workTab.value!.classList.remove("active");
    eduTab.value!.classList.add("active");
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
    eduTab.value!.classList.remove("active");
    workTab.value!.classList.add("active");
  }
};
const toShowQual = ref<Qualification[]>(qualEdu);
onMounted(async () => {
  eduTab.value!.addEventListener("click", () => switchQualTabs("Education"));
  workTab.value!.addEventListener("click", () => switchQualTabs("Work"));
});
</script>

<template>
  <!-- Qualifications Section -->
  <section class="qualifications-section">
    <h2>My Personal Journey</h2>
    <div class="qualifications-container">
      <div class="tabs">
        <div class="education-tab active activate-cursor" ref="eduTab">
          <i class="activate-cursor uil uil-graduation-cap"></i
          ><span class="activate-cursor">Education</span>
        </div>
        <div class="work-tab activate-cursor" ref="workTab">
          <i class="activate-cursor uil uil-briefcase-alt"></i
          ><span class="activate-cursor">Work</span>
        </div>
      </div>
      <div class="sections" ref="qualSection">
        <div class="content" ref="qualContent">
          <div v-for="(item, index) in toShowQual" :key="index" class="leading">
            <div v-if="index % 2 !== 0" class="filler"></div>
            <div v-if="index % 2 !== 0" class="timeline">
              <span class="rounder"></span>
              <span class="line"></span>
            </div>
            <div class="details">
              <h3>{{ item.heading }}</h3>
              <span class="sub-heading">{{ item.subHeading }}</span>
              <span v-html="item.note" class="note"></span>
              <div class="dates">
                <i class="uil uil-calendar-alt"></i>
                <span class="dates justify-self-end self-end">{{ item.dates }}</span>
              </div>
            </div>
            <div v-if="index % 2 === 0" class="timeline">
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
</template>

<style lang="scss" scoped>
@mixin flex($direction, $align, $justify) {
  display: flex;
  flex-direction: $direction;
  align-items: $align;
  justify-content: $justify;
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
          @media screen and (max-width: 600px) {
            @include flex(column, center, center);
            .timeline,
            .filler {
              display: none;
            }
            .details {
              margin: 2rem 0;
            }
          }
          .details {
            width: 100%;
            @include flex(column, flex-start, center);
            background: rgba(0, 0, 0, 0.2);
            border-radius: 1.25rem;
            padding: 2rem;
            h3 {
              font-size: clamp($medium-sub-fs, 2vw, $big-fs);
              color: rgb(26, 211, 211);
            }
            .sub-heading {
              font-size: clamp($small-fs, 2vw, $medium-fs);
              margin-top: 1rem;
            }
            .note {
              font-size: clamp($small-fs, 2vw, $medium-sub-fs);
              margin: 1rem 0 1.5rem;
              opacity: 0.7;
            }
            .dates {
              background: rgba(0, 0, 0, 0.2);
              border-radius: 0.5rem;
              padding: 0.5rem;
              align-self: flex-end;
              font-size: clamp($small-fs, 2vw, $medium-sub-fs);
              opacity: 0.9;
            }
          }
          i {
            margin-right: 1.5rem;
          }
          .timeline {
            .rounder {
              display: inline-block;
              width: 1.3rem;
              height: 1.3rem;
              background: rgb(255, 0, 85);
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

          // .timeline,
          // .filler {
          //   @media screen and (max-width: 600px) {
          //     display: none;
          //   }
          // }
        }
      }
    }
  }
}
</style>
