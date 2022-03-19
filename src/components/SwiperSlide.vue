<template>
  <div>
    <swiper
      :slides-per-view="1"
      :space-between="0"
      :navigation="true"
      :loop="true"
      :autoplay="{
        delay: 1500,
        disableOnInteraction: true,
      }"
      :pagination="{
        clickable: true,
      }"
      :breakpoints="{
        300: {
          slidesPerView: 1,
          spaceBetween: 0,
        },
        576: {
          slidesPerView: 2,
          spaceBetween: 10,
        },
        992: {
          slidesPerView: 3,
          spaceBetween: 20,
        },
        1200: {
          slidesPerView: 4,
          spaceBetween: 25,
        },
      }"
      :modules="modules"
    >
      <swiper-slide v-for="deal of deals" :key="deal.id">
        <img :src="require(`@/assets/${deal.image}`)" />
        <!-- json-server --watch db.json  //run local json server// -->
        <h3 class="cost">{{ deal.cost }}</h3>
        <button :class="deal.btnClass">{{ deal.button }}</button>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import axios from "axios";
const baseURL = "http://localhost:3000/deals";

// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";
import "swiper/css/autoplay";

// import Swiper core and required modules
import { Autoplay, Pagination, Navigation } from "swiper";

export default {
  name: "SwiperSlide",
  components: {
    Swiper,
    SwiperSlide,
  },
  data() {
    return {
      deals: [],
    };
  },
  setup() {
    return {
      modules: [Autoplay, Pagination, Navigation],
    };
  },
  async created() {
    try {
      const res = await axios.get(baseURL);

      this.deals = res.data;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>

<style scoped>
.swiper-slide {
  margin-bottom: 1.5rem;
}
.btn:not(:disabled):not(.disabled) {
  cursor: pointer;
}
[type="reset"],
[type="submit"],
button,
html [type="button"] {
  -webkit-appearance: button;
}
.btn-danger {
  color: #fff;
  background-color: #dc3545;
  border-color: #dc3545;
}
.btn-primary {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}
.btn {
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
button,
select {
  text-transform: none;
}
button,
input {
  overflow: visible;
}
button,
input,
optgroup,
select,
textarea {
  margin: 0;
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
</style>
