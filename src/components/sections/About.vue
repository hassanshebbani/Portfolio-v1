<template>
  <!-- About Section -->
  <section class="about-section" id="about">
    <h2>About Me</h2>
    <div
      class="about-container flex flex-col items-center justify-center lg:grid lg:grid-cols-2 lg:items-start gap-10"
    >
      <img src="/favicon.ico" alt="" />
      <div class="leading flex flex-col items-center justify-center lg:items-start">
        <p class="text-center lg:text-start">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Corrupti
          voluptas quos, eos animi quod sapiente neque, delectus rerum aut at
          minima vel adipisci.
        </p>
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
        <a class="resume w-fit mx-auto justify-self-center lg:justify-self-start lg:mx-0" download target="_blank" href="/sample-pdf.pdf">
          <span>Resume</span><i class="uil uil-download-alt"></i>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts"></script>

<style lang="scss" scoped>
@mixin flex($direction, $align, $justify) {
  display: flex;
  flex-direction: $direction;
  align-items: $align;
  justify-content: $justify;
}

.about-section {
  .about-container {
    img {
      width: 75%;
      border-radius: 1rem;
      justify-self: center;
      align-self: center;
    }
    .leading {
      p {
        font-size: 2rem;
      }
      .about-info {
        @include flex(row, center, space-between);
        width: 80%;
        margin: 2rem 0;
        .info {
          text-align: center;
          p {
            font-size: 2.5rem;
            font-weight: bold;
          }
        }
      }
      .resume {
        background: rgb(2, 184, 184);
        box-shadow: 0 1rem 2rem rgba(0, 255, 255, 0.5);
        cursor: pointer;
        font-size: 1.5rem;
        padding: 1rem 1.5rem;
        border-radius: 1rem;
        text-align: center;
        color: white;
        span {
          margin-right: 2rem;
        }
      }
    }
  }
}
</style>
