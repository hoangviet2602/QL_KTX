<script setup>
import { onMounted } from "vue";

// example components
import DefaultNavbar from "@/examples/navbars/NavbarDefault.vue";
import Header from "@/examples/Header.vue";

//Vue Material Kit 2 components
import MaterialInput from "@/components/MaterialInput.vue";
import MaterialSwitch from "@/components/MaterialSwitch.vue";
import MaterialButton from "@/components/MaterialButton.vue";

// material-input
import setMaterialInput from "@/assets/js/material-input";
import MyNotificaion from '@/components/MyNotification.vue';
import axios from 'axios'
onMounted(() => {
  setMaterialInput();
});
</script>
<template>
  <MyNotificaion v-if="show" :message="notificationMessage" :type="notificationType" @close="hideNotification" />
  <DefaultNavbar transparent />
  <Header>
    <div class="page-header align-items-start min-vh-100" :style="{
      backgroundImage:
        'url(https://images.unsplash.com/photo-1497294815431-9365093b7331?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1950&q=80)'
    }" loading="lazy">
      <span class="mask bg-gradient-dark opacity-6"></span>
      <div class="container my-auto">
        <div class="row">
          <div class="col-lg-4 col-md-8 col-12 mx-auto">
            <div class="card z-index-0 fadeIn3 fadeInBottom">
              <div class="card-header p-0 position-relative mt-n4 mx-3 z-index-2">
                <div class="bg-gradient-success shadow-success border-radius-lg py-3 pe-1">
                  <h4 class="text-white font-weight-bolder text-center mt-2 mb-0">
                    Đăng nhập
                  </h4>
                  <div class="row mt-3">
                    <div class="col-2 text-center ms-auto">
                      <a class="btn btn-link px-3" href="javascript:;">
                        <i class="fa fa-facebook text-white text-lg"></i>
                      </a>
                    </div>

                    <div class="col-2 text-center me-auto">
                      <a class="btn btn-link px-3" href="javascript:;">
                        <i class="fa fa-google text-white text-lg"></i>
                      </a>
                    </div>
                  </div>
                </div>
              </div>
              <div class="card-body">
                <form role="form" class="text-start" methods="post" @submit.prevent="Login">

                  <MaterialInput id="username" class="input-group-outline my-3"
                    :label="{ text: 'Tài khoản', class: 'form-label' }" type="username"
                    @input="data.username = $event.target.value" />
                  <MaterialInput id="password" class="input-group-outline mb-3"
                    :label="{ text: 'Mật khẩu', class: 'form-label' }" type="password"
                    @input="data.password = $event.target.value" />
                  <MaterialSwitch class="d-flex align-items-center mb-3" id="rememberMe" labelClass="mb-0 ms-3" checked>
                    Nhớ tài khoản</MaterialSwitch>

                  <div class="text-center">
                    <MaterialButton class="my-4 mb-2" variant="gradient" color="success" fullWidth>
                      Đăng nhập</MaterialButton>
                  </div>
                  <p class="mt-4 text-sm text-center">
                    Bạn là sinh viên mới?
                    <a href="/pages/landing-pages/register" class="text-success text-gradient font-weight-bold">Đăng
                      kí</a>
                  </p>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
      <footer class="footer position-absolute bottom-2 py-2 w-100">
        <div class="container">
          <div class="row align-items-center justify-content-lg-between">
            <div class="col-12 col-md-6 my-auto">

            </div>

          </div>
        </div>
      </footer>
    </div>
  </Header>
</template>
<script>
export default {
  components: {
 
    MyNotificaion
  },
  data() {
    return {
      data: {
        username: null,
        password: null,
      },
      user: null,   
      // notification
      show: false,
      notificationMessage: '',
      notificationType: '', 
    }
  },
  mounted(){  
  },
  methods: {
    Login() {
      axios.get('https://localhost:7252/api/SV/login/'+this.data.username+"/"+this.data.password, {
       }, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
        }
      })
        .then(response => {
          console.log(response)
          if (response.status === 200) {
            //this.showNotification('Đăng nhập thành công', 'success')
            localStorage.setItem('token', response.data.token);
            localStorage.setItem('userid',response.data.user.id)
            localStorage.setItem('phongid',response.data.user.phongId)
          
            console.log(localStorage.getItem('userid'))
            this.$router.push('/');
          }else{
            this.showNotification('Tài khoản hay mật khẩu không đúng', 'error')
          }
        })
        .catch(error => {
          //console.log(error)
          this.showNotification('Tài khoản hay mật khẩu không đúng', 'error')
          
        });
    },
    showNotification(notificationMessage, notificationType) {
      this.notificationMessage = notificationMessage;
      this.notificationType = notificationType;
      this.show = true;
    },
    hideNotification() {
      this.show = false;
    },
  }
}
</script>