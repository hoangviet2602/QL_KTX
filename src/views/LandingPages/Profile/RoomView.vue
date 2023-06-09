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
import MyNotificaion from '@/components/MyNotification.vue';
//hook

onMounted(() => {
  setNavPills();
  setMaterialInput();
});
</script>
<template>
  <BaseLayout title="" :breadcrumb="[{ label: 'THÔNG TIN PHÒNG CỦA BẠN', route: '#' }]">
  </BaseLayout>
  <MyNotificaion v-if="show" :message="notificationMessage" :type="notificationType" @close="hideNotification" />
  <section>
    <div class="container py-4">

      <div class="row">
        <div class="col-lg-12 mx-0 d-flex justify-content-center flex-column ">
          <h4> Phòng {{ tenPhong }} <p>Số giường : <b>{{ slGiuong }}</b> - Số giường trống : <b>{{ conTrong }}</b></p>
          </h4>
          <div class="card-body">

            <div class="row justify-content-end">

              <MaterialButton variant="gradient" color="success" class="w-auto me-2" @click="showSubform1 = true">Gia hạn
                phòng</MaterialButton>
              <MaterialButton variant="gradient" color="primary" class="w-auto me-2" @click="confirmAction">Hủy phòng
              </MaterialButton>
              <MaterialButton variant="gradient" color="secondary" class="w-auto me-2" @click="showSubform3 = true">Chuyển
                phòng</MaterialButton>

              <!-- Sub form gia hạn phòng -->
              <div v-if="showSubform1" class="backdrop">
                <div class="subform">
                  <div class="row ">
                    <div class="col-sm-9">
                      <h5> Gia hạn Phòng </h5>
                    </div>
                    <div class="col-sm-3 ">
                      <MaterialButton variant="outline" color="dark" class="w-auto me-2" @click="showSubform1 = false">
                        Đóng</MaterialButton>
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-sm-6">
                      <h6 class="mt-3">Chọn kì muốn gia hạn</h6>
                    </div>
                    <div class="col-sm-4">
                      <select class="form-select mt-2" @change.prevent="SelectKi">
                        <option v-for="option in ki" :key="option.ki.idKi" :value="option.ki.idKi">{{ option.ki.mota +
                          ' / ' + option.nam }}
                        </option>
                      </select>

                    </div>
                  </div>
                  <div class="row mt-3">
                    <div class="col-sm-6">
                      <label>
                        <input type="radio" name="check_room" value="option1" v-model="selectedOption" 
                        @change="handleRadioChange">
                        Tiếp tục ở phòng cũ
                      </label>
                    </div>

                     <div class="col-sm-6">
                      <label>
                        <input type="radio" name="check_room" value="option2" v-model="selectedOption" 
                        @change="handleRadioChange">
                        Chuyển sang phòng mới
                      </label>
                      <div v-if="selectedOption === 'option2'">
                        <select class="form-select " @change.prevent="SelectKhu">
                        <option v-for="option in khu" :key="option.idKhu" :value="option.idKhu">{{ option.tenKhu }}
                        </option>
                      </select>
                      <select class="form-select mt-2" @change.prevent="SelectPhong">
                        <option v-for="option in phongs" :key="option.idPhong" :value="option.idPhong">{{ option.tenphong
                        }}(Còn trống: {{ option.conTrong }})
                        </option>
                      </select>
                      </div>
                    </div>
                  </div>
                  <div class="row col-sm-8 mx-auto d-flex justify-content-center flex-column mt-4">
                    <MaterialButton variant="gradient" color="success" class="w-auto me-2"
                      @click="GiaHanPhong(), showSubform1 = false">Xác nhận</MaterialButton>
                  </div>
                </div>
              </div>
              <!-- Sub form chuyển phòng -->
              <div v-if="showSubform3" class="backdrop">
                <div class="subform">

                  <div class="row ">
                    <div class="col-sm-9">
                      <h5> Chuyển phòng </h5>
                    </div>
                    <div class="col-sm-3 ">
                      <MaterialButton variant="outline" color="dark" class="w-auto me-2" @click="showSubform3 = false">
                        Đóng</MaterialButton>
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-sm-5">
                      <h6>Chọn khu</h6>
                      <h6 class="mt-4">Chọn phòng </h6>
                    </div>
                    <div class="col-sm-5">
                      <select class="form-select " @change.prevent="SelectKhu">
                        <option v-for="option in khu" :key="option.idKhu" :value="option.idKhu">{{ option.tenKhu }}
                        </option>
                      </select>
                      <select class="form-select mt-2" @change.prevent="SelectPhong">
                        <option v-for="option in phongs" :key="option.idPhong" :value="option.idPhong">{{ option.tenphong
                        }}(Còn trống: {{ option.conTrong }})
                        </option>
                      </select>

                    </div>
                  </div>
                  <div class="row col-sm-8 mx-auto d-flex justify-content-center flex-column mt-4">
                    <MaterialButton variant="gradient" color="success" class="w-auto me-2" @click.prevent="ChuyenPhong">
                      Xác nhận</MaterialButton>
                  </div>
                </div>
              </div>
            </div>
            <div class="row border border-dark">

              <div class="col-lg-5 mx-0 ">
                <h4>SINH VIÊN CÙNG PHÒNG</h4>
                <div class="card bg-light w-auto m-3" v-for="item in sinhVienCungPhong" :key="item.id">
                  <div class="info-block">
                    <div class="image-container">
                      <img :src="'../../src/assets/img/' + item.sv.anh3x4" alt="Image" class="img-fluid rounded-circle"
                        width="80px">
                    </div>
                    <div class="info-content">
                      <h5>{{ item.sv.hoten }}</h5>
                      <p class="lead">{{ item.name }}</p>
                    </div>
                  </div>
                </div>
              </div>

              <div class="col-lg-6 mx-auto ">
                <h4>YÊU CẦU CỦA BẠN</h4>
                <div class="yeucau-container" v-for="item in paginatedItems" :key="item.idYC">
                  <div class="yeucau">
                    <p class="yeucau-info" v-if="item.loaiYc == 1">Loại yêu cầu: <b style="color: darkgray;">Chuyển
                        phòng</b></p>
                    <p class="yeucau-info" v-if="item.loaiYc == 2">Loại yêu cầu: <b style="color: darkgreen;">Gia hạn
                        phòng</b></p>
                    <p class="yeucau-info" v-if="item.loaiYc == 3">Loại yêu cầu: <b style="color: crimson;">Hủy phòng</b>
                    </p>

                    <p class="yeucau-info" v-if="item.status == 0">Trạng thái: Đang chờ</p>
                    <p class="yeucau-info" v-if="item.status == 1">Trạng thái: Đã phê duyệt</p>
                    <p class="yeucau-info" v-if="item.status == -1">Trạng thái: Đã từ chối</p>

                    <p class="yeucau-info" v-if="item.loaiYc == 1">Phòng chuyển đến: {{ item.tenPhongMoi }}</p>
                    <p class="yeucau-info" v-if="item.loaiYc == 2">Kì gia hạn: {{ item.thoiGianGiaHan }}</p>
                    <p class="yeucau-info" v-if="item.loaiYc == 3">Kì gia hạn: {{ item.thoiGianHuy }}</p>
                  </div>
                  <div class="yeucau">
                    <span class="yeucau-value" id="ngay-gui"> {{ moment(item.thoigiangui).format('DD/MM/yyy') }} </span>
                  </div>
                </div>
                <div class="pagination-container">
                  <div class="pagination">
                    <a @click="previousPage" :disabled="currentPage === 1">&laquo;</a>
                    <a v-for="page in totalPages" :key="page" :class="{ active: page === currentPage }"
                      @click="goToPage(page)">
                      {{ page }}
                    </a>
                    <a @click="nextPage" :disabled="currentPage === totalPages">&raquo;</a>
                  </div>
                </div>
              </div>

            </div>
          </div>
        </div>
      </div>

    </div>

  </section>
</template>

<style>
.yeucau-container {
  border: 1px solid #ccc;
  padding: 5px;
  position: relative;
  border-radius: 10px;
  margin-top: 10px;
}

.yeucau {
  margin-bottom: 2px;
}

.yeucau-info {
  font-weight: bold;
}

.yeucau-value {
  position: absolute;
  top: 0;
  right: 0;
  margin-top: 5px;
  margin-right: 10px;
  color: blue;
}

.subform {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999;
  background-color: white;
  width: 400px;
  height: auto;
  padding: 5px;
  border-radius: 10px;
}

.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9998;
}

.info-block {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
}

.image-container img {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  margin-right: 10px;
}

.info-content {
  flex: 1;
}

.info-block:hover {
  background-color: #f0f0f0;
}

.info-block:active {
  transform: scale(0.95);
}

.pagination-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.pagination {
  display: inline-block;
  align-items: center;
}

.pagination a {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
  cursor: pointer;

}

.pagination a.active {
  background-color: #4CAF50;
  color: white;
  border-radius: 5px;

}

.pagination a:hover:not(.active) {
  background-color: #ddd;
  border-radius: 5px;
}
</style>
<script>
import axios from 'axios'
import moment from 'moment'
export default {
  components: {
    MyNotificaion
  },
  computed: {
    paginatedItems() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.yeucauphong.slice(startIndex, endIndex);
    },
    totalPages() {
      return Math.ceil(this.yeucauphong.length / this.itemsPerPage);
    },
  },
  data() {
    return {
      moment,
      showSubform1: false,
      showSubform3: false,
      sinhVienCungPhong: [],
      ki: [],
      khu: [],
      phongs: [],
      kihientai: [],
      yeucauphong: [],
      selectedKi: '',
      selectedKhu: '',
      selectedPhong: '',
      selectedPhongGiaHan:'',
      tenPhong: 'Bạn chưa được xếp phòng',
      slGiuong: 0,
      conTrong: 0,
      // notification
      show: false,
      notificationMessage: '',
      notificationType: '',
      // phân trang
      listRoom: [],
      currentPage: 1, // The current page number
      itemsPerPage: 3, // The number of items to display per page
      selectedOption: 'option1'
    }
  },
  methods: {
    handleRadioChange() {
   
      console.log('Selected option:', this.selectedOption);
      console.log(this.RadioPhong())

    },
    RadioPhong(){
      if(this.selectedOption === 'option1'){
          return localStorage.getItem('phongid')
      }else{
        return this.selectedPhong
      }
    },
    confirmAction() {
      const currentDate = new Date();
      const formattedDate = currentDate.toISOString();
      if (confirm("Bạn có chắc muốn gửi yêu cầu hủy phòng không?")) {
        // loaiyc = 3
        axios.post('https://localhost:7252/api/YeuCauPhongs', {
          thoigiangui: formattedDate,// set df in db
          loaiYc: 3,
          status: 0,
          kiHuyId: this.kihientai[0].idKi,
          sinhVienId: localStorage.getItem('userid'),
          phongId: localStorage.getItem('phongid')
        })
          .then(response => {
            console.log(response.data)
            this.showNotification('Gửi yêu cầu hủy phòng thành công', 'success')
            this.getYeuCauPhong()
          }).catch(error => {
            console.log(error)
          })
      } else {

      }
    },
    SelectKi(event) {
      this.selectedKi = event.target.value;
      console.log(this.selectedKi)
    },
    SelectKhu() {
      this.selectedKhu = event.target.value;
      console.log(this.selectedKhu)
      // get phòng còn trống
      axios.get('https://localhost:7252/api/Phongs/avai_room/' + this.selectedKhu)
        .then(response => {
          console.log(response.data)
          this.phongs = response.data
        }).catch(error => {
          console.log(error)
        })
    },
    SelectPhong(event) {
      this.selectedPhong = event.target.value
      console.log(this.selectedPhong)
    },
    GiaHanPhong() {
      const currentDate = new Date();
      const formattedDate = currentDate.toISOString();
      // loaiyc = 2
      console.log(formattedDate)
      axios.post('https://localhost:7252/api/YeuCauPhongs', {
        thoigiangui: formattedDate,
        loaiYc: 2,
        status: 0,
        kiGiaHanId: this.selectedKi,
        sinhVienId: localStorage.getItem('userid'),

        phongId: this.RadioPhong()
      })
        .then(response => {
          console.log(response.data)
          this.showNotification('Gửi yêu cầu gia hạn thành công', 'success')
          this.getYeuCauPhong()
        }).catch(error => {
          console.log(error)
        })
    },
    ChuyenPhong() {
      const currentDate = new Date();
      const formattedDate = currentDate.toISOString();

      // loại yc = 1
      if (localStorage.getItem('phongid') == this.selectedPhong) {
        alert("Phòng chuyển đến trùng với phòng hiện tại");
      } else {
        axios.post('https://localhost:7252/api/YeuCauPhongs', {
          thoigiangui: formattedDate,
          loaiYc: 1,
          status: 0,
          idNewRoom: this.selectedPhong,
          sinhVienId: localStorage.getItem('userid'),
          phongId: localStorage.getItem('phongid')
        })
          .then(response => {
            console.log(response.data)
            this.showNotification('Gửi yêu cầu chuyển phòng thành công', 'success')
            this.getYeuCauPhong()
          }).catch(error => {
            console.log(error)

          })
        this.showSubform3 = false;
      }
    },
    showNotification(notificationMessage, notificationType) {
      this.notificationMessage = notificationMessage;
      this.notificationType = notificationType;
      this.show = true;
    },
    hideNotification() {
      this.show = false;
    },
    getYeuCauPhong() {
      axios.get('https://localhost:7252/api/YeuCauPhongs/YcPhongSv/' + localStorage.getItem('userid'))
        .then(response => {
          console.log(response.data)
          this.yeucauphong = response.data
        }).catch(error => {
          console.log(error)
        })
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    goToPage(page) {
      this.currentPage = page;
    },
  },

  mounted() {
    this.getYeuCauPhong()
    axios.get('https://localhost:7252/api/SinhViens/sv-cungphong/' + localStorage.getItem('phongid'))
      .then(response => {
        console.log(response.data)
        this.sinhVienCungPhong = response.data
      }).catch(error => {
        console.log(error)
      })
    // get kì
    axios.get('https://localhost:7252/api/Kis')
      .then(response => {
        console.log(response.data)
        this.ki = response.data
      }).catch(error => {
        console.log(error)
      })

    // get khu
    axios.get('https://localhost:7252/api/Khus')
      .then(response => {
        console.log(response.data)

        this.khu = response.data
      }).catch(error => {
        console.log(error)
      })
    // get phòng của sinh viên
    axios.get('https://localhost:7252/api/Phongs/' + localStorage.getItem('phongid'))
      .then(response => {
        console.log(response.data)
        this.tenPhong = response.data.tenphong
        this.slGiuong = response.data.slgiuong
        this.conTrong = this.slGiuong - parseInt(response.data.slSv)
      }).catch(error => {
        console.log(error)
      })
    // get kì hiện tại
    axios.get('https://localhost:7252/api/Kis/KiHienTai')
      .then(response => {
        console.log(response.data)
        this.kihientai = response.data
        console.log(this.kihientai[0].idKi)
      }).catch(error => {
        console.log(error)
      })

  }
}
</script>

