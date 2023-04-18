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

//hook
onMounted(() => {
  setNavPills();
  setMaterialInput();
});
</script>
<template>
  <BaseLayout title="" :breadcrumb="[{ label: 'ĐĂNG KÍ THÔNG TIN Ở KÍ TÚC XÁ ĐẠI HỌC SƯ PHẠM KỸ THUẬT', route: '#' }]">
  </BaseLayout>

  <section>
    <div class="container py-4">
      <form role="form" id="contact-form" method="post" autocomplete="off">
        <div class="row">


          <!-- khối thông tin sinh viên bên trái -->
          <div class="col-lg-7 mx-0 d-flex justify-content-center flex-column ">
            <h4>THÔNG TIN SINH VIÊN</h4>

            <div class="card-body">
              <div class="row">
                <div class="col-md-6">
                  <MaterialInput class="input-group-dynamic mb-2" :label="{ text: 'Họ tên lót(*)', class: 'form-label' }"
                    type="text" />
                </div>
                <div class="col-md-6 ps-2">
                  <MaterialInput class="input-group-dynamic" :label="{ text: 'Tên(*)', class: 'form-label' }"
                    type="text" />
                </div>
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-dynamic" :label="{ text: 'Giới tính(*)', class: 'form-label' }"
                  type="text" />
              </div>
              <div class="row">
                <div class="col-md-6">
                  <MaterialInput class="input-group-dynamic mb-2" :label="{ text: 'Dân tộc(*)', class: 'form-label' }"
                    type="text" />
                </div>
                <div class="col-md-6 ps-2">
                  <MaterialInput class="input-group-dynamic" :label="{ text: 'Tôn giáo', class: 'form-label' }"
                    type="text" />
                </div>
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-dynamic" :label="{ text: 'CCCD(*)', class: 'form-label' }"
                  type="text" />
              </div>
              <div class="col-md-6 ">
                <MaterialInput class="input-group-static" label="Ngày cấp CCCD(*)" type="date" />
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-dynamic" :label="{ text: 'Nơi cấp CCCD(*)', class: 'form-label' }"
                  type="text" />
              </div>
              <p class=""><b>Diện chính sách</b></p>
              <div class="row">
                <div class="col-md-3">
                  <label class="form-check-label">Hộ nghèo</label>
                  <input type="checkbox" value="" id="defaultCheck1">
                </div>
                <div class="col-md-3 ps-3">
                  <label for="option1">Con thương binh</label>
                  <input type="checkbox" id="option1" name="options" value="1">
                </div>
                <div class="col-md-3 ps-3">
                  <label for="option1">Con liệt sĩ</label>
                  <input type="checkbox" id="option1" name="options" value="1">
                </div>
                <div class="col-md-3 ps-3">
                  <label for="option1">Mồ côi cha,mẹ</label>
                  <input type="checkbox" id="option1" name="options" value="1">
                </div>
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-static " label="Email(*)" type="email"
                  placeholder="Nhập đúng để nhận mã xác nhận" />
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-dynamic" :label="{ text: 'Số điện thoại(*)', class: 'form-label' }"
                  type="text" />
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-static " label="Mã sinh viên" type="email"
                  placeholder="Nếu chưa có thì bỏ qua" />
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Trường(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="selectpicker">
                    <option>--Trống--</option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Khoa(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="selectpicker">
                    <option>--Trống--</option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Sinh viên năm(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="selectpicker">
                    <option>--Trống--</option>
                  </select>
                </div>
              </div>

            </div>
            <h4>HỘ KHẨU THƯỜNG TRÚ</h4>
            <div class="card-body">

              <div class="row">
                <div class="col-md-4">
                  <p>Tình/Thành phố(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="selectpicker">
                    <option>--Trống--</option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Quận/Huyện(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="selectpicker">
                    <option>--Trống--</option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Phường/Xã(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="selectpicker">
                    <option>--Trống--</option>
                  </select>
                </div>
              </div>
              <div class="col-md-12 mb-2">
                <MaterialInput class="input-group-dynamic"
                  :label="{ text: 'Số nhà, tên đường, tổ/xóm, khu phố/thôn/ấp ', class: 'form-label' }" type="text" />
              </div>






            </div>
          </div>
          <!-- khối bên phải -->
          <div class="col-lg-5 mx-0 d-flex align-items-center flex-column ">
            <h4>HÌNH ẢNH MINH CHỨNG</h4>
            <div class="card-body ">
              <h6>Ảnh 3x4(<span class="text-danger">*</span>)</h6>
              <div class="d-flex justify-content-center align-items-center img-thumbnail"
                style="width: 150px; height: 150px;">
                <img src="path/to/image.jpg" alt="Image" style="max-width: 100%; max-height: 80%;">
              </div>
              <MaterialButton variant="gradient" color="dark" class="w-auto me-2 mt-2">Chọn ảnh</MaterialButton>

              <h6>Ảnh CCCD mặt sau(<span class="text-danger">*</span>)</h6>
              <div class="d-flex justify-content-center align-items-center img-thumbnail"
                style="width: 150px; height: 150px;">
                <img src="path/to/image.jpg" alt="Image" style="max-width: 100%; max-height: 80%;">
              </div>
              <MaterialButton variant="gradient" color="dark" class="w-auto me-2 mt-2">Chọn CCCD mặt trước
              </MaterialButton>

              <h6>Ảnh CCCD mặt sau(<span class="text-danger">*</span>)</h6>
              <div class="d-flex justify-content-center align-items-center img-thumbnail"
                style="width: 150px; height: 150px;">
                <img src="path/to/image.jpg" alt="Image" style="max-width: 100%; max-height: 80%;">
              </div>
              <MaterialButton variant="gradient" color="dark" class="w-auto me-2 mt-2">Chọn CCCD mặt sau</MaterialButton>


              <div class="row">
                <div class="col-lg-7">
                  <h6>Mã xác thực<p>(Được gửi qua mail)</p>
                  </h6>
                </div>

              </div>
              <div class="row">

                <div class="col-lg-8 ">
                  <MaterialInput class="input-group-dynamic" :label="{ text: 'Nhập mã xác thực', class: 'form-label' }"
                    type="text" />
                </div>
                <div class="col-lg-4">
                  <Button style="width: auto; height: 30px;border-radius: 5px;background-color: cadetblue;">
                    Lấy mã</Button>
                </div>
              </div>
            </div>


          </div>

        </div>
        <div class="row ">
          <div class="col-md-12  ">
            <MaterialSwitch class="mb-4 " id="flexSwitchCheckDefault" checked labelClass="ms-3 mb-0">
              Tôi cam kết tất cả nội dung khai báo trên là đúng sự thật
            </MaterialSwitch>
            <div class="col-md-4 mx-auto ">
              <MaterialButton type=" " variant="gradient" color="dark" fullWidth>Gửi</MaterialButton>
            </div>
          </div>
        </div>
      </form>
    </div>
  </section>
</template>
<script>
window.addEventListener('load', function () {
  let elements = document.getElementsByTagName('label');
  for (let i = 0; i < elements.length; i++) {
    if (elements[i].textContent.includes('*')) {
      elements[i].innerHTML = elements[i].innerHTML.replace('*', '<span class="text-danger">*</span>');
    }
  }
});
</script>
