<template>
    <li class="bg-white px-4 py-6 shadow rounded-sm">
        <div class="flex justify-center">
          <div class="min-w-fit mx-auto">
            <img class="inline-block w-10 rounded-full" :src="course.image_url" :alt="course.title">
          </div>
          <div class="w-10/12">
            <div class="flex">
              <div class="flex-1 overflow-flex-wrap">
                <h2 class="text-xl font-bold text-gray-900 mb-1">
                  <router-link :to="{ name: 'single-course', params: { courseType: type, slug:course.slug}}" class="text-blue-500 hover:underline">{{ course.title }}</router-link>
                </h2>
                <div class="flex items-center gap-3">
                  <div class="flex items-center space-x-px">
                     <ReviewStar :star="avarageStar" />
                  </div>
                  <span class="text-sm text-gray-500">{{ courtRvw }} Reviews</span>
                </div>
              </div>
            </div>
            <div class="mt-4 space-y-1 text-sm text-gray-700 line-clamp-5">
              <p>{{ description }}</p>
            </div>
            <div class="mt-6">
              <div class="flex flex-col">
                <div class="flex space-x-0 gap-2 flex-wrap justify-items-start">
                  <div class="inline-flex items-center gap-2 text-sm text-gray-500">
                    <svg class="w-6 h-6 text-gray-400 shrink-0" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M3 13.125C3 12.504 3.504 12 4.125 12h2.25c.621 0 1.125.504 1.125 1.125v6.75C7.5 20.496 6.996 21 6.375 21h-2.25A1.125 1.125 0 013 19.875v-6.75zM9.75 8.625c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125v11.25c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V8.625zM16.5 4.125c0-.621.504-1.125 1.125-1.125h2.25C20.496 3 21 3.504 21 4.125v15.75c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V4.125z"></path>
                    </svg>
                    <span>{{ course.level.name }}</span>
                  </div>
                  <div v-if="course.resources >0" class="inline-flex items-center gap-2 text-sm text-gray-500">
                    <svg class="w-6 h-6 text-gray-400 shrink-0" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M3.375 19.5h17.25m-17.25 0a1.125 1.125 0 01-1.125-1.125M3.375 19.5h1.5C5.496 19.5 6 18.996 6 18.375m-3.75 0V5.625m0 12.75v-1.5c0-.621.504-1.125 1.125-1.125m18.375 2.625V5.625m0 12.75c0 .621-.504 1.125-1.125 1.125m1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125m0 3.75h-1.5A1.125 1.125 0 0118 18.375M20.625 4.5H3.375m17.25 0c.621 0 1.125.504 1.125 1.125M20.625 4.5h-1.5C18.504 4.5 18 5.004 18 5.625m3.75 0v1.5c0 .621-.504 1.125-1.125 1.125M3.375 4.5c-.621 0-1.125.504-1.125 1.125M3.375 4.5h1.5C5.496 4.5 6 5.004 6 5.625m-3.75 0v1.5c0 .621.504 1.125 1.125 1.125m0 0h1.5m-1.5 0c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125m1.5-3.75C5.496 8.25 6 7.746 6 7.125v-1.5M4.875 8.25C5.496 8.25 6 8.754 6 9.375v1.5m0-5.25v5.25m0-5.25C6 5.004 6.504 4.5 7.125 4.5h9.75c.621 0 1.125.504 1.125 1.125m1.125 2.625h1.5m-1.5 0A1.125 1.125 0 0118 7.125v-1.5m1.125 2.625c-.621 0-1.125.504-1.125 1.125v1.5m2.625-2.625c.621 0 1.125.504 1.125 1.125v1.5c0 .621-.504 1.125-1.125 1.125M18 5.625v5.25M7.125 12h9.75m-9.75 0A1.125 1.125 0 016 10.875M7.125 12C6.504 12 6 12.504 6 13.125m0-2.25C6 11.496 5.496 12 4.875 12M18 10.875c0 .621-.504 1.125-1.125 1.125M18 10.875c0 .621.504 1.125 1.125 1.125m-2.25 0c.621 0 1.125.504 1.125 1.125m-12 5.25v-5.25m0 5.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125m-12 0v-1.5c0-.621-.504-1.125-1.125-1.125M18 18.375v-5.25m0 5.25v-1.5c0-.621.504-1.125 1.125-1.125M18 13.125v1.5c0 .621.504 1.125 1.125 1.125M18 13.125c0-.621.504-1.125 1.125-1.125M6 13.125v1.5c0 .621-.504 1.125-1.125 1.125M6 13.125C6 12.504 5.496 12 4.875 12m-1.5 0h1.5m-1.5 0c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125M19.125 12h1.5m0 0c.621 0 1.125.504 1.125 1.125v1.5c0 .621-.504 1.125-1.125 1.125m-17.25 0h1.5m14.25 0h1.5"></path>
                    </svg>
                    <span>{{ course.resources }} videos</span>
                  </div>
                  <div class="inline-flex items-center gap-2 text-sm text-gray-500">
                    <svg class="w-6 h-6 text-gray-400 shrink-0" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                    </svg>
                    <span>{{ course.duration == 0 ? '1-5 hours' : course.duration == 1 ? '5-10 hours' : '10+ hours' }}</span>
                  </div>
                  <div class="inline-flex items-center gap-2 text-sm text-gray-500">
                    <svg class="w-6 h-6 text-gray-400 shrink-0" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v12m-3-2.818l.879.659c1.171.879 3.07.879 4.242 0 1.172-.879 1.172-2.303 0-3.182C13.536 12.219 12.768 12 12 12c-.725 0-1.45-.22-2.003-.659-1.106-.879-1.106-2.303 0-3.182s2.9-.879 4.006 0l.415.33M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                    </svg>
                    <span>{{ course.price <1 ? "Free": ` $${course.price}.00` }}</span>
                  </div>
                </div>
              </div>
            </div>
            <div class="mt-6 flex justify-between space-x-8"></div>
          </div>
          <div class="flex w-1/12 overflow-hidden justify-end">
              <vue-gravatar class="inline-block h-8 w-8 rounded-full ring-2 ring-white" :email="course.submitted_by.email" :size="30" />
          </div>
        </div>
    </li>
</template>


<script>
import ReviewStar from './ReviewStar.vue';
export default{
  name: 'CoursesItem',
  components: {
    ReviewStar
  },
  props: ['course', 'type'],
  data() {
    return {
      description: '',
      avarageStar: 0,
      courtRvw:0,
    }
  },
  mounted() {
    this.shortDescription();
    this.reviwsCalculation(this.course.reviews)
  },

  methods: {
    shortDescription() {
      const words = this.course.description.split(' ');  
      const getWord = words.slice(0, 20); 
      const srtDescription = getWord.join(' ');

      this.description = srtDescription;
    },
    reviwsCalculation(reviews) {
      if (Array.isArray(reviews)) {
        let totalStar = reviews.reduce((prev, current) => {
          return prev + current.star;
        }, 0);

        this.avarageStar = Math.round(totalStar / reviews.length);
        this.courtRvw = reviews.length;
      }
    }
  }
}
</script>