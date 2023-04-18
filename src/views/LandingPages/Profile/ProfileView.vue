<script setup>
import { onMounted } from "vue";



// Sections components
import BaseLayout from "@/layouts/sections/components/BaseLayout.vue";


// Inputs page components
import InputStatic from "@/layouts/sections/input-areas/inputs/components/InputStatic.vue";
import MaterialInput from "@/components/MaterialInput.vue";

import MaterialTextArea from "@/components/MaterialTextArea.vue";
import MaterialButton from "@/components/MaterialButton.vue";
import MaterialSwitch from "@/components/MaterialSwitch.vue";
//nav-pills & material-input
import setNavPills from "@/assets/js/nav-pills";
import setMaterialInput from "@/assets/js/material-input";

import MaterialSocialButton from "@/components/MaterialSocialButton.vue";
//hook
onMounted(() => {
  setNavPills();
  setMaterialInput();
});
</script>
<template>
  <BaseLayout title="" :breadcrumb="[{ label: 'THÔNG TIN SINH VIÊN', route: '#' }]">
  </BaseLayout>

  <section>
    <div class="container py-4">
      <form role="form" id="contact-form" method="post" autocomplete="off">
        <div class="row">


          <!-- khối thông tin sinh viên bên trái -->
          <div class="col-lg-12 mx-0 d-flex justify-content-center flex-column ">
            <h4>THÔNG TIN SINH VIÊN</h4>

            <div class="container">
              <div class="row">
                <div class="col-lg-4 mx-0">
                  <div class="nav-wrapper position-relative end-0">
                    <ul class="nav nav-pills nav-fill p-1" role="tablist">
                      <li class="nav-item">
                        <a class="nav-link mb-0 px-0 py-1 active" data-bs-toggle="tab" href="#profile-tabs-simple"
                          role="tab" aria-controls="profile" aria-selected="true">
                        Thông tin cá nhân
                        </a>
                      </li>
                      <li class="nav-item">
                        <a class="nav-link mb-0 px-0 py-1" data-bs-toggle="tab" href="#dashboard-tabs-simple" role="tab"
                          aria-controls="dashboard" aria-selected="false">
                        Thông tin cư trú
                        </a>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>


            <div class="col-lg-12 mx-0 d-flex justify-content-center flex-column ">
              <!-- cotent -->
              <div class="tab-content ">
                <div class="tab-pane fade show active pd-2 " id="profile-tabs-simple" role="tabpanel"
                  aria-labelledby="profile-tab">
                  <!-- ảnh -->
                  <div class="row">
                    <div class="col-lg-4 mx-auto  border-right ">
                      <div class="mx-auto img-thumbnail" style="width: 350px; height: 350px;">
                        <img src="@/assets/img/bruce-mars.jpg" alt="Image" style="max-width: 100%; max-height: 100%;">
                      </div>
                    </div>
                    <!-- info -->
                    <div class="col-lg-8 mx-0  ">

                      <h4 class="">NGUYỄN HOÀNG VIỆT</h4>
                      <table class="table">
                        <tbody>
                          <tr>
                            <th scope="row">Ngày sinh</th>
                            <td>26/02/2001</td>            
                          </tr>
                          <tr>
                            <th scope="row">Giới tính</th>
                            <td>JNam</td>  
                          </tr>
                          <tr>
                            <th scope="row">Điện thoại sinh viên</th>
                            <td>0768570252</td>
                          </tr>
                          <tr>
                            <th scope="row">SV năm</th>
                            <td>5</td>
                          </tr>
                          <tr>
                            <th scope="row">Sinh viên trường</th>
                            <td>Đại học Sư Phạm Kỹ Thuật Đà Nẵng</td>
                          </tr>
                          <tr>
                            <th scope="row">Khoa</th>
                            <td>Công nghệ số</td>
                          </tr>
                          <tr>
                            <th scope="row">Mã sinh viên</th>
                            <td>1911505310169</td>
                          </tr><tr>
                            <th scope="row">Mã ký túc xá</th>
                            <td>101A1911505310169</td>
                          </tr>
                          <tr>
                            <th scope="row">Tôn giáo</th>
                            <td>không</td>
                          </tr>
                          <tr>
                            <th scope="row">Dân tộc</th>
                            <td>Kinh</td>
                          </tr>
                          <tr>
                            <th scope="row">Quốc gia</th>
                            <td>Việt Nam</td>
                          </tr>
                          <tr>
                            <th scope="row">CCCD</th>
                            <td>1234124123</td>
                          </tr>
                          <tr>
                            <th scope="row">Ngày cấp CCCD</th>
                            <td>20/1/2021</td>
                          </tr>
                          <tr>
                            <th scope="row">Nơi cấp CCCD</th>
                            <td>Huế</td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                  </div>

                </div>
                <div class="tab-pane fade" id="dashboard-tabs-simple" role="tabpanel" aria-labelledby="dashboard-tab">
              
                </div>
              </div>
            </div>
          </div>

        </div>
      </form>

    </div>
  </section>
</template>


<style>
.table tbody th{
  font-weight: normal;
}
.table tbody tr td{
  text-transform: uppercase;
  font-weight: bold;
}
</style>
