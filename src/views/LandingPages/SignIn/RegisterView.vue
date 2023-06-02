<script setup>
import { onMounted } from "vue";

// Sections components
import BaseLayout from "@/layouts/sections/components/BaseLayout.vue";

// Inputs page components
import InputStatic from "@/layouts/sections/input-areas/inputs/components/InputStatic.vue";
import MaterialInput from "@/components/MaterialInput.vue";
import MaterialAlert from "../../../components/MaterialAlert.vue";
import MaterialTextArea from "@/components/MaterialTextArea.vue";
import MaterialButton from "@/components/MaterialButton.vue";
import MaterialSwitch from "@/components/MaterialSwitch.vue";
import MyNotificaion from '@/components/MyNotification.vue';
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
  <MyNotificaion v-if="show" :message="notificationMessage" :type="notificationType" @close="hideNotification" />

  <BaseLayout title="" :breadcrumb="[{ label: 'ĐĂNG KÍ THÔNG TIN Ở KÍ TÚC XÁ ĐẠI HỌC SƯ PHẠM KỸ THUẬT', route: '#' }]">
  </BaseLayout>
  <div>

  </div>
  <section>
    <div class="container py-4">
      <form role="form" id="contact-form" method="post" @submit="submitForm">
        <div class="row">


          <!-- khối thông tin sinh viên bên trái -->
          <div class="col-lg-7 mx-0 d-flex justify-content-center flex-column ">
            <h4>THÔNG TIN SINH VIÊN</h4>

            <div class="card-body">
              <div class="row">
                <div class="col-md-12">
                  <MaterialInput class="input-group-dynamic mb-2" :label="{ text: 'Họ và tên(*)', class: 'form-label', }"
                    type="text" @input="hoten = $event.target.value" />
                </div>

              </div>
              <div class="row mt-2 mb-1">
                <div class="col-md-4">
                  <p>Giói tính(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-3 ps-2">
                  <select class="form-select" @change.prevent="SelectGioitinh">
                    <option v-for="option in gioitinh" :key="option.label" :value="option.value">{{ option.label }}
                    </option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-6">
                  <MaterialInput class="input-group-dynamic mb-2" :label="{ text: 'Dân tộc(*)', class: 'form-label' }"
                    type="text" @input="dantoc = $event.target.value" />
                </div>
                <div class="col-md-6 ps-2">
                  <MaterialInput class="input-group-dynamic" :label="{ text: 'Tôn giáo', class: 'form-label' }"
                    type="text" @input="tongiao = $event.target.value" />
                </div>
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-dynamic" :label="{ text: 'CCCD(*)', class: 'form-label' }" type="text"
                  @input="cccd = $event.target.value" />
              </div>
              <div class="col-md-6 ">
                <MaterialInput class="input-group-static" label="Ngày cấp CCCD(*)" type="date"
                  @input="ngaycap = $event.target.value" />
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-dynamic" :label="{ text: 'Nơi cấp CCCD(*)', class: 'form-label' }"
                  type="text" @input="noicap = $event.target.value" />
              </div>
              <p class=""><b>Diện chính sách</b></p>
              <div class="row">
                <div class="col-md-3">
                  <input type="checkbox" id="myCheckbox1" v-model="isPoor">
                  <label for="myCheckbox1">Hộ nghèo</label>
                </div>
                <div class="col-md-4">
                  <input type="checkbox" id="myCheckbox2" v-model="isWarVeteran">
                  <label for="myCheckbox2">Con thương binh</label>
                </div>
                <div class="col-md-3">
                  <input type="checkbox" id="myCheckbox3" v-model="isMartyr">
                  <label for="myCheckbox3">Con liệt sĩ</label>
                </div>
                <div class="col-md-3">
                  <input type="checkbox" id="myCheckbox4" v-model="isOrphan">
                  <label for="myCheckbox4">Mồ côi cha/mẹ</label>
                </div>
                <div class="col-md-3">
                  <input type="checkbox" id="myCheckbox5" v-model="isNone">
                  <label for="myCheckbox5">Không</label>
                </div>
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-static " label="Email(*)" type="email"
                  placeholder="Nhập đúng để nhận mã xác nhận" @input="email = $event.target.value" />
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-static " label="Số điện thoại(*)" type="text"
                  placeholder="Nhập số điện thoại của bạn" @input="phone = $event.target.value" />
              </div>
              <div class="col-md-6 mb-2">
                <MaterialInput class="input-group-static " label="Mã sinh viên" type="text"
                  placeholder="Nếu chưa có thì bỏ qua" @input="masinhvien = $event.target.value" />
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Trường(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="form-select" @change.prevent="SelectTruong">
                    <option v-for="option in truong" :key="option.truongId" :value="option.truongId">{{ option.name }}
                    </option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Ngành học(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <MaterialInput class="input-group-dynamic" :label="{ text: '', class: 'form-label' }" type="text"
                    @input="nganhhoc = $event.target.value" />
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Sinh viên năm(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="form-select mt-2" @change.prevent="SelectNam">
                    <option v-for="option in namhoc" :key="option.value" :value="option.value">{{ option.label }}</option>
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
                  <select class="form-select mt-2" @change.prevent="SelectTinh_TP">
                    <option v-for="option in tinh_TP" :key="option.code" :value="option.code">{{ option.name_with_type }}
                    </option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Quận/Huyện(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="form-select mt-2" @change.prevent="SelectQuanHuyen">
                    <option v-for="option in quan_huyen" :key="option.code" :value="option.code">{{ option.name_with_type
                    }}
                    </option>
                  </select>
                </div>
              </div>
              <div class="row">
                <div class="col-md-4">
                  <p>Phường/Xã(<span class="text-danger">*</span>)</p>
                </div>
                <div class="col-md-8 ps-2">
                  <select class="form-select mt-2" @change.prevent="SelectPhuongXa">
                    <option v-for="option in xa_phuong" :key="option.code" :value="option.code">{{ option.name_with_type
                    }}
                    </option>
                  </select>
                </div>
              </div>
              <div class="col-md-12 mt-2 mb-4">
                <MaterialInput class="input-group-dynamic"
                  :label="{ text: 'Số nhà, tên đường, tổ/xóm, khu phố/thôn/ấp ', class: 'form-label' }" type="text"
                  @input="thon = $event.target.value" />
              </div>

            </div>
          </div>
          <!-- khối bên phải -->
          <div class="col-lg-5 mx-0 d-flex align-items-center flex-column ">
            <h4>HÌNH ẢNH MINH CHỨNG</h4>
            <div class="card-body ">
              <!-- ảnh 3x4 -->
              <h6>Ảnh 3x4(<span class="text-danger">*</span>)</h6>
              <div class="d-flex justify-content-center align-items-center img-thumbnail"
                style="width: 150px; height: 150px;">
                <img v-if="anh3x4" :src="anh3x4" alt="Image" style="max-width: 100%; max-height: 80%;">
              </div>
              <MaterialButton variant="gradient" color="dark" class="w-auto me-2 mt-2" @click.prevent="chooseFile1">Chọn
                ảnh</MaterialButton>
              <input type="file" accept=".jpg" ref="fileInput1" style="display: none" @change="handleFileChange1">
              <!-- căn cước công dân trước -->
              <h6>Ảnh CCCD mặt sau(<span class="text-danger">*</span>)</h6>
              <div class="d-flex justify-content-center align-items-center img-thumbnail"
                style="width: 150px; height: 150px;">
                <img v-if="cccdtruocimg" :src="cccdtruocimg" alt="Image" style="max-width: 100%; max-height: 80%;">
              </div>
              <MaterialButton type="file" variant="gradient" color="dark" class="w-auto me-2 mt-2"
                @click.prevent="chooseFile2">Chọn CCCD mặt trước
              </MaterialButton>
              <input type="file" accept=".jpg" ref="fileInput2" style="display: none" @change="handleFileChange2">
              <!-- căn cước công dân sau -->
              <h6>Ảnh CCCD mặt sau(<span class="text-danger">*</span>)</h6>
              <div class="d-flex justify-content-center align-items-center img-thumbnail"
                style="width: 150px; height: 150px;">
                <img v-if="cccdsauimg" :src="cccdsauimg" alt="Image" style="max-width: 100%; max-height: 80%;">
              </div>
              <MaterialButton type="file" variant="gradient" color="dark" class="w-auto me-2 mt-2"
                @click.prevent="chooseFile3">Chọn CCCD mặt sau</MaterialButton>
              <input type="file" accept=".jpg" ref="fileInput3" style="display: none" @change="handleFileChange3">

              <div class="row">
                <div class="col-lg-7">
                  <h6>Mã xác thực<p>(Được gửi qua mail)</p>
                  </h6>
                </div>

              </div>
              <div class="row">

                <div class="col-lg-8 ">
                  <MaterialInput class="input-group-dynamic" :label="{ text: 'Nhập mã xác thực', class: 'form-label' }"
                    type="text" @input="code = $event.target.value" />
                </div>
                <div class="col-lg-4">
                  <Button style="width: auto; height: 30px;border-radius: 5px;background-color: cadetblue;" @click.prevent="LayMa">
                    Lấy mã</Button>
                </div>
              </div>
            </div>


          </div>

        </div>
        <div class="row ">
          <div class="col-md-12  ">
            <MaterialSwitch class="mb-4 " id="checkboxSubmit" labelClass="ms-3 mb-0" v-model="isConfirm"
              :checked="isConfirm" @update:checked="isConfirm = $event">
              Tôi cam kết tất cả nội dung khai báo trên là đúng sự thật
            </MaterialSwitch>
            <div class="col-md-4 mx-auto ">
              <MaterialButton :disabled="!isConfirm" variant="gradient" color="dark" fullWidth>Gửi</MaterialButton>
            </div>
          </div>
        </div>
      </form>
    </div>
  </section>
</template>
<script>
import axios from 'axios'

export default {
  components: {
    MaterialButton,
    MyNotificaion
  },
  data() {
    return {
      isConfirm: true,
      cccdsauimg: null,
      cccdtruocimg: null,
      anh3x4: null,
      tinh_TP: [],
      quan_huyen: [],
      xa_phuong: [],
      selectedDistric: 0,
      selectedQuan_huyen: 0,
      SelectedPhuongXa: 0,
      tenTinh: '',
      tenHuyen: '',
      tenXa: '',
      diachi: '',
      truong: [],
      namhoc: [
        { label: 'Năm 1', value: 1 },
        { label: 'Năm 2', value: 2 },
        { label: 'Năm 3', value: 3 },
        { label: 'Năm 4', value: 4 },
        { label: 'Năm 5', value: 5 }
      ],
      gioitinh:
        [
          { label: 'Nam', value: 1 },
          { label: 'Nữ', value: 2 },
          { label: 'Khác', value: 0 },
        ],
      selectedTruong: '',
      nganh: '',
      selectedNam: 0,
      hoten: '',
      selectedGioiTinh: 0,
      dantoc: '',
      tongiao: '',
      cccd: '',
      ngaycap: '',
      noicap: '',
      email: '',
      phone: '',
      masinhvien: '',
      thon: '',
      // notification
      show: false,
      notificationMessage: '',
      notificationType: '',
      //checkbox
      isPoor: false,
      isWarVeteran: false,
      isMartyr: false,
      isOrphan: false,
      isNone: false,
      codeFromServer:0,
      code:0
    }
  },
  methods: {
    SelectGioitinh(event) {
      this.selectedGioiTinh = event.target.value;
    },
    SelectTruong(event) {
      this.selectedTruong = event.target.value;
    },
    SelectNam(event) {
      this.selectedNam = event.target.value;
    },
    chooseFile1() {
      this.$refs.fileInput1.click();
    },
    chooseFile2() {
      this.$refs.fileInput2.click();
    },
    chooseFile3() {
      this.$refs.fileInput3.click();
    },
    handleFileChange1(event) {
      this.anh3x4 = event.target.files[0];
      const file = event.target.files[0];
      const reader = new FileReader();
      reader.onload = () => {
        this.anh3x4 = reader.result;
        console.log(this.anh3x4)
      };
      reader.readAsDataURL(file);
    },
    handleFileChange2(event) {
      this.cccdtruocimg = event.target.files[0];
      const file = event.target.files[0];
      const reader = new FileReader();
      reader.onload = () => {
        this.cccdtruocimg = reader.result;
        console.log(this.cccdtruocimg)
      };
      reader.readAsDataURL(file);
    },
    handleFileChange3(event) {
      this.cccdsauimg = event.target.files[0];
      const file = event.target.files[0];
      const reader = new FileReader();
      reader.onload = () => {
        this.cccdsauimg = reader.result;
        console.log(this.cccdsauimg)
      };
      reader.readAsDataURL(file);
    },
    showNotification(notificationMessage, notificationType) {
      this.notificationMessage = notificationMessage;
      this.notificationType = notificationType;
      this.show = true;
    },
    hideNotification() {
      this.show = false;
    },
    submitForm(event) {
      event.preventDefault()
      if(this.code == this.codeFromServer){
        this.sendFormDataToServer();
      }else{
        this.showNotification('Mã xác nhận không đúng', 'error')
      }
    },
    LayMa(){
      if(this.email == ''){
        this.showNotification('Email trống', 'error')
      }else{
        axios.get('https://localhost:7252/api/Email?nguoinhan=' + this.email)
        .then(respone => {
         this.codeFromServer = respone.data 
          console.log(this.codeFromServer)
        }).catch(error => {
          console.log(error)
        })
      }
    },
    sendFormDataToServer() {
      axios.post('https://localhost:7252/api/DonDangKies', {
        hoten: this.hoten,
        phone: this.phone,
        dob: "2023-05-22T08:51:32.597Z",
        status: 0,
        gioitinh: this.selectedGioiTinh,
        namhoc: this.selectedNam,
        nganhhoc: this.nganhhoc,
        masinhvien: this.masinhvien,
        tonGiao: this.tongiao,
        quocTich: this.dantoc,
        dienchinhsach: this.getDienChinhSachValue(),
        cccd: this.cccd,
        ngaycap: this.ngaycap,
        noicap: this.noicap,
        email: this.email,
        truongId: this.selectedTruong,
        anhCccdMatsau: this.cccdsauimg,
        anhcccdMattruoc: this.cccdtruocimg,
        anh3x4: this.anh3x4,
        hoKhauThuongTru: this.thon + ', ' + this.tenXa + ', ' + this.tenHuyen + ', ' + this.tenTinh
      })
        .then(response => {
          console.log(response.data);
          this.showNotification('Gửi đơn đăng kí thành công', 'success')
          this.$router.push('/');
        })
        .catch(error => {
          console.error(error);
        });
    },
    SelectTinh_TP(event) {
      this.selectedDistric = event.target.value;
      const foundObject = this.tinh_TP.find(item => item.code === this.selectedDistric);
      this.tenTinh = foundObject ? foundObject.name_with_type : "";

      axios.get('https://vn-public-apis.fpo.vn/districts/getByProvince?provinceCode=' + this.selectedDistric + '&limit=-1')
        .then(respone => {
          this.quan_huyen = respone.data.data.data
          console.log(this.quan_huyen)
        }).catch(error => {
          console.log(error)
        })
    },
    SelectQuanHuyen(event) {
      this.selectedQuan_huyen = event.target.value;
      const foundObject = this.quan_huyen.find(item => item.code === this.selectedQuan_huyen);
      this.tenHuyen = foundObject ? foundObject.name_with_type : "";

      axios.get('https://vn-public-apis.fpo.vn/wards/getByDistrict?districtCode=' + this.selectedQuan_huyen + '&limit=-1')
        .then(respone => {
          this.xa_phuong = respone.data.data.data
          console.log(this.xa_phuong)
        }).catch(error => {
          console.log(error)
        })
    },
    SelectPhuongXa(event) {
      this.SelectedPhuongXa = event.target.value;
      const foundObject = this.xa_phuong.find(item => item.code === this.SelectedPhuongXa);
      this.tenXa = foundObject ? foundObject.name_with_type : "";

      console.log(this.thon + ', ' + this.tenXa + ', ' + this.tenHuyen + ', ' + this.tenTinh)
    },
    getDienChinhSachValue() {
      const isPoor = this.isPoor;
      const isWarVeteran = this.isWarVeteran;
      const isMartyr = this.isMartyr;
      const isOrphan = this.isOrphan;
      const isNone = this.isNone; 
      var dienChinhSach = "";
      if (isPoor) {
        dienChinhSach += "Hộ nghèo |";
      }
      if (isWarVeteran) {
        dienChinhSach += "Con thương binh |";
      }
      if (isMartyr) {
        dienChinhSach += " Con liệt sĩ |";
      }
      if (isOrphan) {
        dienChinhSach += " Mồ côi cha/mẹ |";
      }
      if (isNone) {
        dienChinhSach += "Không ";
      }
      console.log(dienChinhSach)
      return dienChinhSach;
    }

  },
  mounted() {
    axios.get('https://localhost:7252/api/Universities')
      .then(respone => {
        this.truong = respone.data
      }).catch(error => {
        console.log(error)
      })
    axios.get('https://vn-public-apis.fpo.vn/provinces/getAll?limit=-1')
      .then(respone => {
        this.tinh_TP = respone.data.data.data
        console.log(this.tinh_TP)
      }).catch(error => {
        console.log(error)
      })
  }
}
window.addEventListener('load', function () {
  let elements = document.getElementsByTagName('label');
  for (let i = 0; i < elements.length; i++) {
    if (elements[i].textContent.includes('*')) {
      elements[i].innerHTML = elements[i].innerHTML.replace('*', '<span class="text-danger">*</span>');
    }
  }
});
</script>

