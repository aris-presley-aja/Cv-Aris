<template>
  <div>
    <Header
      :resume-url="navbar.resumeUrl"
      :external-links="navbar.externalLinks"
    />
    <main class="main">
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-12 col-md-10 col-lg-8 col-xl-7 col-xxl-6">
            <section class="">
              <div class="contact__heading text-center my-3">
                <h1>Course & Certificate</h1>
              </div>
<!-- <NuxtImg
  provider="cloudinary"
  src="images/ninja.png"
  alt="image of my site"
  loading="lazy"
  preset="blog"
  width="640"
  height="480"
  sizes="sm:355px md:320px lg:480px"
  class="images"
/> -->
<!-- <nuxt-img src="./asset/images/ninja.png" /> -->

              <!-- Add your custom action here (i.e. formspree.io) -->
                             <div
                  v-for="certified in Certified"
                  :key="certified.id"
                  class="col-12 col-md-10 col-lg-6 col-xl-5 mb-4 mb-lg-5"
                >
                               <Certified
                    :title="certified.title"
                    :description="certified.description"
                    :image="certified.image"
                  />
                             </div>
              <hr />

            </section>
          </div>
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    async asyncData({ $content }) {
    const certified = (await $content('Certified').fetch()).sort(
      // Sort by projects by id in ascending order
      (a: any, b: any) => {
        if (a.id > b.id) {
          return 1
        }
        if (a.id < b.id) {
          return -1
        }
        return 0
      }
    )
    const navbar = await $content('navbar').fetch()
    return {
      certified,
      navbar,
    }
  },
  head: {
    title: 'Course - Aris Priyanto',
  },
})
</script>

<style lang="scss" scoped>
@import '@/scss/abstracts';
.contact {
  padding: pxToRem(10);
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: space-between;


  // &__form {
  // }

  &__label {
    color: $gray-6;
    font-size: pxToRem(15);
  }
  &__input {
    min-height: pxToRem(45);
  }
  &__input,
  &__textarea {
    transition: border 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
    border: 1px solid rgba($gray-2, 0.7);
    @include hocus {
      border: 1px solid rgba($primary, 0.3);
      box-shadow: 0 0 pxToRem(5) 0 rgba($primary, 0.2);
    }
  }
}
</style>
