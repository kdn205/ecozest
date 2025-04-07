<template>
    <div>
      <div class="w-full">
        <!-- Header -->
        <header class="flex items-center justify-between p-4 border-b bg-white shadow-md fixed top-0 left-0 w-full z-10">
          <div class="text-lg text-green font-bold w-1/4">LOGO HERE</div>
          <nav class="hidden md:flex flex-1 justify-center">
            <div class="flex items-center space-x-12">
              <a href="#" class="hover:text-green-600 transition-colors duration-200 py-2">Home</a>
              <div
                class="relative"
                @mouseenter="showStoryDropdown"
                @mouseleave="hideStoryDropdownWithDelay"
              >
                <a href="#" class="hover:text-green-600 transition-colors duration-200 py-2">Our Story</a>
                <div
                  ref="storyDropdown"
                  class="absolute hidden flex-col bg-white shadow-md border mt-2 rounded min-w-[150px] left-1/2 -translate-x-1/2"
                  @mouseenter="cancelHideStoryDropdown"
                  @mouseleave="hideStoryDropdownWithDelay"
                >
                  <a href="#" class="block px-4 py-2 hover:bg-green-50 hover:text-green-600 transition-colors duration-200 text-center">About us</a>
                  <a href="#" class="block px-4 py-2 hover:bg-green-50 hover:text-green-600 transition-colors duration-200 text-center">Our Vision</a>
                  <a href="#" class="block px-4 py-2 hover:bg-green-50 hover:text-green-600 transition-colors duration-200 text-center">Our Team</a>
                </div>
              </div>
              <div
                class="relative"
                @mouseenter="showProductDropdown"
                @mouseleave="hideProductDropdownWithDelay"
              >
                <a href="#" class="hover:text-green-600 transition-colors duration-200 py-2">Our Product</a>
                <div
                  ref="productDropdown"
                  class="absolute hidden flex-col bg-white shadow-md border mt-2 rounded min-w-[150px] left-1/2 -translate-x-1/2"
                  @mouseenter="cancelHideProductDropdown"
                  @mouseleave="hideProductDropdownWithDelay"
                >
                  <a href="#" class="block px-4 py-2 hover:bg-green-50 hover:text-green-600 transition-colors duration-200 text-center">Cleaning</a>
                  <a href="#" class="block px-4 py-2 hover:bg-green-50 hover:text-green-600 transition-colors duration-200 text-center">Spray</a>
                  <a href="#" class="block px-4 py-2 hover:bg-green-50 hover:text-green-600 transition-colors duration-200 text-center">Car Care</a>
                </div>
              </div>
              <a href="#" class="hover:text-green-600 transition-colors duration-200 py-2">Contact Us</a>
            </div>
          </nav>
          <div class="flex space-x-2 w-1/4 justify-end">
            <input type="text" placeholder="Search" class="border p-2 rounded bg-gray-50 w-48 text-black hidden md:block" />
            <!-- Hamburger Menu -->
            <button class="md:hidden" @click="toggleMobileMenu">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
              </svg>
            </button>
          </div>
        </header>

        <!-- Mobile Menu -->
        <div v-if="isMobileMenuOpen" class="md:hidden fixed top-0 left-0 w-full h-full bg-black/50 z-20">
          <div class="bg-white w-3/4 h-full p-4">
            <button class="mb-4" @click="toggleMobileMenu">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
            <ul class="space-y-4">
              <li><a href="#" class="block text-black hover:text-green-600">Home</a></li>
              <li><a href="#" class="block text-black hover:text-green-600">Our Story</a></li>
              <li><a href="#" class="block text-black hover:text-green-600">Our Product</a></li>
              <li><a href="#" class="block text-black hover:text-green-600">Contact Us</a></li>
            </ul>
          </div>
        </div>

        <!-- Slideshow Section -->
        <section class="mt-2 relative overflow-hidden">
          <div class="relative h-[456px] max-w-[736px] mx-auto">
            <transition-group name="slide" tag="div" class="relative h-full w-full">
                <div v-for="(slide, index) in slides" :key="slide.id" v-show="currentSlide === index" 
                     class="absolute w-full h-full">
                  <img :src="slide.image" :alt="slide.title" class="w-full h-full object-cover">
                </div>
              </transition-group>
              <!-- Navigation Arrows -->
              <button @click="prevSlide" class="absolute left-4 top-1/2 -translate-y-1/2 bg-black/30 hover:bg-black/50 text-white p-2 rounded-full transition-all duration-300">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                </svg>
              </button>
              <button @click="nextSlide" class="absolute right-4 top-1/2 -translate-y-1/2 bg-black/30 hover:bg-black/50 text-white p-2 rounded-full transition-all duration-300">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
              </button>
              <!-- Navigation Dots -->
              <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex space-x-2">
                <button v-for="(slide, index) in slides" :key="slide.id"
                        @click="currentSlide = index"
                        class="w-3 h-3 rounded-full transition-all duration-300"
                        :class="currentSlide === index ? 'bg-white scale-125' : 'bg-white/50'">
                      </button>
                    </div>
                  </div>
                </section>
                <main>
                 <section class="mt-8 text-center">
                   <a class="text-green-600 font-semibold text-sm" href="https://www.facebook.com/nugtyi/">Thương Hiệu của Ecozest trên Shopee</a>
                 </section>
                
          <!--product section-->
        <main class="pt-5 px-5 flex items-center justify-center bg-white">
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-6 text-center">
              <div class="flex flex-col items-center justify-center border rounded-lg p-4">
                <img src="../assets/logo/logo-tag.jpg" alt="Icon 1" class="w-12 h-12 mb-2" />
                <p class="font-semibold text-black">Sử dụng vỏ bưởi</p>
              </div>
              <div class="flex flex-col items-center justify-center border rounded-lg p-4">
                <img src="../assets/logo/logo-tag.jpg" alt="Icon 2" class="w-12 h-12 mb-2" />
                <p class="font-semibold text-black">Thành phần tự nhiên</p>
              </div>
              <div class="flex flex-col items-center justify-center border rounded-lg p-4">
                <img src="../assets/logo/logo-tag.jpg" alt="Icon 3" class="w-12 h-12 mb-2" />
                <p class="font-semibold text-black">An Toàn Sức Khỏe</p>
              </div>
              <div class="flex flex-col items-center justify-center border rounded-lg p-4">
                <img src="../assets/logo/logo-tag.jpg" alt="Icon 4" class="w-12 h-12 mb-2" />
                <p class="font-semibold text-black">Thân Thiện Môi Trường</p>
              </div>
              <div class="flex flex-col items-center justify-center border rounded-lg p-4">
                <img src="../assets/logo/logo-tag.jpg" alt="Icon 5" class="w-12 h-12 mb-2" />
                <p class="font-semibold text-black">Trạm refill</p>
              </div>
              <div class="flex flex-col items-center justify-center border rounded-lg p-4">
                <img src="../assets/logo/logo-tag.jpg" alt="Icon 6" class="w-12 h-12 mb-2" />
                <p class="font-semibold text-black">Hỗ trợ giao hàng</p>
              </div>
            </div>
          </main>

          <div class="mt-8 text-center px-4 font-semibold text-black">
            <p> Sản phẩm của Ecozest là sự kết hợp giữa các thành phần từ thiên nhiên cùng với tinh đầu 
              <br>và hợp chất khoáng tạo nên sự phong cách và độc đáo cho sản phẩm .
            </p>
          </div>
  
          <section class="mt-8">
            <h2 class="text-center text-green-600 font-semibold text-lg">Best Seller Products</h2>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mt-4">
              <div class="w-full h-40 bg-gray-300 overflow-hidden">
                <img src="../assets/pr_img/crazybear.jpg" class="w-full h-full object-cover">
              </div>
              <div class="w-full h-40 bg-gray-300 overflow-hidden">
                <img src="../assets/pr_img/crazydeadlin.jpg" class="w-full h-full object-cover">
              </div>
              <div class="w-full h-40 bg-gray-300 overflow-hidden">
                <img src="../assets/pr_img/crazygus.jpg" class="w-full h-full object-cover">
              </div>
              <div class="w-full h-40 bg-gray-300 overflow-hidden">
                <img src="../assets/pr_img/doggo.jpg" class="w-full h-full object-cover">
              </div>
            </div>
          </section>
  

          
          <section class="mt-8">
            <h2 class="text-green-600 font-semibold text-lg">News</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
              <div class="w-full h-32 bg-gray-300"></div>
              <div class="w-full h-32 bg-gray-300"></div>
              <div class="w-full h-32 bg-gray-300"></div>
              <div class="w-full h-32 bg-gray-300"></div>
            </div>
          </section>
        </main>
      </div>
    </div>
</template>

<script>
export default {
  name: "EcozestPage",
  data() {
    return {
      storyHideTimeout: null,
      productHideTimeout: null,
      currentSlide: 0,
      slides: [
        {
          id: 1,
          image: '/land_img/img-1.jpg', // Ensure this path is correct
          title: 'Ecozest Landing'
        },
        {
          id: 2,
          image: '/land_img/img-2.jpg',
          title: 'Ecozest Products'
        },
        {
          id: 3,
          image: '/land_img/img-3.jpg',
          title: 'Ecozest Vision'
        }
      ],
      slideInterval: null,
      isMobileMenuOpen: false, // State for mobile menu
    };
  },
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen;
    },
    showStoryDropdown() {
      const dropdown = this.$refs.storyDropdown;
      if (dropdown) {
        dropdown.classList.remove("hidden");
      }
      if (this.storyHideTimeout) {
        clearTimeout(this.storyHideTimeout);
        this.storyHideTimeout = null;
      }
    },
    hideStoryDropdownWithDelay() {
      this.storyHideTimeout = setTimeout(() => {
        const dropdown = this.$refs.storyDropdown;
        if (dropdown) {
          dropdown.classList.add("hidden");
        }
      }, 200);
    },
    cancelHideStoryDropdown() {
      if (this.storyHideTimeout) {
        clearTimeout(this.storyHideTimeout);
        this.storyHideTimeout = null;
      }
    },
    showProductDropdown() {
      const dropdown = this.$refs.productDropdown;
      if (dropdown) {
        dropdown.classList.remove("hidden");
      }
      if (this.productHideTimeout) {
        clearTimeout(this.productHideTimeout);
        this.productHideTimeout = null;
      }
    },
    hideProductDropdownWithDelay() {
      this.productHideTimeout = setTimeout(() => {
        const dropdown = this.$refs.productDropdown;
        if (dropdown) {
          dropdown.classList.add("hidden");
        }
      }, 200);
    },
    cancelHideProductDropdown() {
      if (this.productHideTimeout) {
        clearTimeout(this.productHideTimeout);
        this.productHideTimeout = null;
      }
    },
    prevSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.slides.length) % this.slides.length;
    },
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.slides.length;
    },
    startSlideshow() {
      this.slideInterval = setInterval(this.nextSlide, 5000);
    },
    stopSlideshow() {
      if (this.slideInterval) {
        clearInterval(this.slideInterval);
        this.slideInterval = null;
      }
    }
  },
  mounted() {
    this.startSlideshow();
  },
  beforeUnmount() {
    this.stopSlideshow();
    if (this.storyHideTimeout) {
      clearTimeout(this.storyHideTimeout);
    }
    if (this.productHideTimeout) {
      clearTimeout(this.productHideTimeout);
    }
  }
};
</script>

<style scoped>
/* Add padding to the main content to avoid overlapping with the fixed header */
main {
  padding-top: 2rem; /* Adjust as needed to match the header height */
}

/* Slideshow Transitions */
.slide-enter-active,
.slide-leave-active {
  transition: all 0.8s ease-in-out;
}

.slide-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.slide-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-enter-to,
.slide-leave-from {
  transform: translateX(0);
  opacity: 1;
}

/* Add styles for the mobile menu overlay */
</style>
