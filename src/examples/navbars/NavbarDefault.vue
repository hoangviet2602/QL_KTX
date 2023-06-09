<script setup>
import { RouterLink } from "vue-router";
import { ref, watch } from "vue";
import { useWindowsWidth } from "../../assets/js/useWindowsWidth";

// images
import ArrDark from "@/assets/img/down-arrow-dark.svg";
import downArrow from "@/assets/img/down-arrow.svg";
import DownArrWhite from "@/assets/img/down-arrow-white.svg";

const props = defineProps({
  action: {
    type: Object,
    route: String,
    color: String,
    label: String,
    default: () => ({
      route: "https://www.creative-tim.com/product/vue-material-kit",
      color: "bg-gradient-success",
      label: "Free Download"
    })
  },
  transparent: {
    type: Boolean,
    default: false
  },
  light: {
    type: Boolean,
    default: false
  },
  dark: {
    type: Boolean,
    default: false
  },
  sticky: {
    type: Boolean,
    default: false
  },
  darkText: {
    type: Boolean,
    default: false
  }
});

// set arrow  color
function getArrowColor() {
  if (props.transparent && textDark.value) {
    return ArrDark;
  } else if (props.transparent) {
    return DownArrWhite;
  } else {
    return ArrDark;
  }
}

// set text color
const getTextColor = () => {
  let color;
  if (props.transparent && textDark.value) {
    color = "text-dark";
  } else if (props.transparent) {
    color = "text-white";
  } else {
    color = "text-dark";
  }

  return color;
};

// set nav color on mobile && desktop

let textDark = ref(props.darkText);
const { type } = useWindowsWidth();

if (type.value === "mobile") {
  textDark.value = true;
} else if (type.value === "desktop" && textDark.value == false) {
  textDark.value = false;
}

watch(
  () => type.value,
  (newValue) => {
    if (newValue === "mobile") {
      textDark.value = true;
    } else {
      textDark.value = false;
    }
  }
);
</script>
<template>
  <nav
    class="navbar navbar-expand-lg top-0"
    :class="{
      'z-index-3 w-100 shadow-none navbar-transparent position-absolute my-3':
        props.transparent,
      'my-3 blur border-radius-lg z-index-3 py-2 shadow py-2 start-0 end-0 mx-4 position-absolute mt-4':
        props.sticky,
      'navbar-light bg-white py-3': props.light,
      ' navbar-dark bg-gradient-dark z-index-3 py-3': props.dark
    }"
  >
    <div
      :class="
        props.transparent || props.light || props.dark
          ? 'container'
          : 'container-fluid px-0'
      ">
      <img src="@/assets/img/logo_spkt-removebg-preview.png " alt="Alternative text" >
      <RouterLink
        class="navbar-brand d-none d-md-block"
        :class="[
          (props.transparent && textDark.value) || !props.transparent
            ? 'text-dark font-weight-bolder ms-sm-3'
            : 'text-white font-weight-bolder ms-sm-3'
        ]"
        :to="{ name: 'presentation' }"
        rel="tooltip"
        title="Designed and Coded by Creative Tim"
        data-placement="bottom">
   <h6> TRUNG TÂM QUẢN LÝ KÝ TÚC XÁ <br> ĐẠI HỌC SƯ PHẠM KỸ THUẬT ĐÀ NẴNG </h6>
      </RouterLink>
      <RouterLink
        class="navbar-brand d-block d-md-none"
        :class="
          props.transparent || props.dark
            ? 'text-white'
            : 'font-weight-bolder ms-sm-3'
        "
        to="/"
        rel="tooltip"
        title="Designed and Coded by Creative Tim"
        data-placement="bottom"
      >
        Material Design AAA
      </RouterLink>
      <a
        href="https://www.creative-tim.com/product/vue-material-kit-pro"
        class="btn btn-sm bg-gradient-success mb-0 ms-auto d-lg-none d-block"
        >Buy Now</a
      >
      <button
        class="navbar-toggler shadow-none ms-2"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navigation"
        aria-controls="navigation"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon mt-2">
          <span class="navbar-toggler-bar bar1"></span>
          <span class="navbar-toggler-bar bar2"></span>
          <span class="navbar-toggler-bar bar3"></span>
        </span>
      </button>
      <div
        class="collapse navbar-collapse w-100 pt-3 pb-2 py-lg-0"
        id="navigation">
        <ul class="navbar-nav navbar-nav-hover ms-auto">
          <!-- LI TRANG CHỦ -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a
              role="button"
              class="nav-link ps-2 d-flex cursor-pointer align-items-center"
              :class="getTextColor()"
              href="#"
              @click.prevent="gotoHome"
              id="dropdownMenuPages"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              <i
                class="material-icons opacity-6 me-2 text-md"
                :class="getTextColor()">home</i>
              TRANG CHỦ
              <img
                :src="getArrowColor()"
                alt="down-arrow"
                class="arrow ms-1 d-lg-none d-block ms-auto"/>
            </a>
            
          </li>
          <!-- LI GIỚI THIỆU -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a
              role="button"
              class="nav-link ps-2 d-flex cursor-pointer align-items-center"
              :class="getTextColor()"
              id="dropdownMenuBlocks"
              data-bs-toggle="dropdown"
              aria-expanded="false">
              <i
                class="material-icons opacity-6 me-2 text-md"
                :class="getTextColor()">view_day</i>
              GIỚI THIỆU
              
              <img
                :src="getArrowColor()"
                alt="down-arrow"
                class="arrow ms-1 d-lg-none d-block ms-auto"/>
            </a>
            
          </li>
          <!-- LI THONG BÁO -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a
              role="button"
              class="nav-link ps-2 d-flex cursor-pointer align-items-center"
              :class="getTextColor()"
              id="dropdownMenuDocs"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              <i
                class="material-icons opacity-6 me-2 text-md"
                :class="getTextColor()"
                >notifications</i>
              THÔNG BÁO
              <img
                :src="getArrowColor()"
                alt="down-arrow"
                class="arrow ms-1 d-lg-none d-block ms-auto"
              />
            </a>
            <!-- <div
              class="dropdown-menu dropdown-menu-end dropdown-menu-animation dropdown-md dropdown-md-responsive p-3 border-radius-lg mt-0 mt-lg-3"
              aria-labelledby="dropdownMenuBlocks">
              <div class="d-none d-lg-block">
                <ul class="list-group">
                  <li class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0 w-20">
                      <div class="d-flex">
                        <div class="w-30 d-flex align-items-center justify-content-between">
                          <div>
                            <h6 class="dropdown-header text-dark font-weight-bolder  p-0 ">
                              Yêu cầu chuyển phòng 
                            </h6>
                            <p class="dropdown-header text-dark  d-flex justify-content-center p-0 ">
                              Yêu cầu chuyển phòng của bạn đã được phê duyệt. 
                              Vui lòng xem chi tiết ở phòng của bạn.
                            </p>
                          </div>
                        </div>
                      </div>
                  </li>
                  <li class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0 w-20">
                      <div class="d-flex">
                        <div class="w-30 d-flex align-items-center justify-content-between">
                          <div>
                            <h6 class="dropdown-header text-dark font-weight-bolder d-flex justify-content-center p-0 ">
                              Yêu cầu chuyển phòng của bạn đã được phê duyệt
                            </h6>
                          </div>
                        </div>
                      </div>
                  </li>
                </ul>
              </div>
         
            </div> -->
          </li>
          <!-- LI ĐĂNG NHẬP -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <!-- Đã login -->
            <div v-if="isLoggedIn">
              <li class="nav-item dropdown dropdown-hover mx-2">
            <a
              role="button"
              class="nav-link ps-2 d-flex cursor-pointer align-items-center"
              :class="getTextColor()"
              id="dropdownMenuBlocks"
              data-bs-toggle="dropdown"
              aria-expanded="false">
              <i
                class="material-icons opacity-6 me-2 text-md"
                :class="getTextColor()">view_day</i>
              TÀI KHOẢN
              <img
                :src="getArrowColor()"
                alt="down-arrow"
                class="arrow ms-1 d-lg-none d-block ms-auto"/>
            </a>
            <div
              class="dropdown-menu dropdown-menu-end dropdown-menu-animation dropdown-md dropdown-md-responsive p-3 border-radius-lg mt-0 mt-lg-3"
              aria-labelledby="dropdownMenuBlocks">
              <div class="d-none d-lg-block">
                <ul class="list-group">
                  <li
                    class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a
                      class="dropdown-item py-2 ps-3 border-radius-md"
                      href="#" @click.prevent="goToProfile">
                      <div class="d-flex">
                        <div
                          class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6 class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                              Thông tin của bạn
                            </h6>
                          </div>
                          <img
                            :src="downArrow"
                            alt="down-arrow"
                            class="arrow"/>
                        </div>
                      </div>
                    </a>
                  </li>
                  <li
                    class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a
                      class="dropdown-item py-2 ps-3 border-radius-md"
                      @click.prevent="goToRoom">
                      <div class="d-flex">
                        <div
                          class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6 class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                             Phòng của bạn
                            </h6>
                          </div>
                          <img
                            :src="downArrow"
                            alt="down-arrow"
                            class="arrow"/>
                        </div>
                      </div>
                    </a>
                  </li>
                  <li
                    class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a
                      class="dropdown-item py-2 ps-3 border-radius-md"
                      @click.prevent="goToBill">
                      <div class="d-flex">
                        <div
                          class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6 class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                           Thanh toán phí
                            </h6>          
                          </div>
                          <img
                            :src="downArrow"
                            alt="down-arrow"
                            class="arrow"/>
                        </div>
                      </div>
                    </a>
                  </li>
                  <li
                    class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a
                      class="dropdown-item py-2 ps-3 border-radius-md"
                      href="#" @click.prevent="Logout">
                      <div class="d-flex">
                        <div
                          class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6 class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                            Đăng xuất
                            </h6>
                          </div>
                          <img  :src="downArrow"
                                alt="down-arrow"
                                class="arrow"/>
                        </div>
                      </div>
                    </a>
                  </li>       
                </ul>
              </div>
              <!-- ?? -->   
            </div>
          </li>
            </div>
            <!-- chưa login -->
            <div v-else>
              <a 
              role="button"
              class="nav-link ps-2 d-flex cursor-pointer align-items-center"
              :class="getTextColor()"
              id="dropdownMenuDocs"
              data-bs-toggle="dropdown"
              aria-expanded="false"
              @click.prevent="goToLogin">         
              <i class="material-icons opacity-6 me-2 text-md"
                :class="getTextColor()">login</i> ĐĂNG NHẬP
            </a>
          </div>
          </li>
        </ul>  
      </div>
    </div>
  </nav>
  <!-- End Navbar --> 
</template>
<script>
export default {
  methods: {
    goToLogin() {
      this.$router.push('/pages/landing-pages/basic');
    }, 
    gotoHome() {
      this.$router.push('/');
    }, 
    goToRoom() {
      this.$router.push('/pages/landing-pages/room');
    },
    goToProfile() {
      this.$router.push('/pages/landing-pages/profile');
    },
    goToBill() {
      this.$router.push('/pages/landing-pages/bill');
    },
    Logout(){
      this.isLoggedIn=false 
      localStorage.removeItem('token');
      localStorage.removeItem('userid');
      this.$router.push('/');
    }
  },
  data() {
    return {
      isLoggedIn: false, // Khởi tạo biến isLoggedIn với giá trị ban đầu là false
    }
  },
  mounted() {
    const token = localStorage.getItem('token');
    console.log(token)
    if (token) {
      this.isLoggedIn = true; 
    } 
  }
}
</script>