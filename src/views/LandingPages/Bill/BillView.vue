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
    <BaseLayout title="" :breadcrumb="[{ label: 'HÓA ĐƠN CỦA BẠN', route: '#' }]">
    </BaseLayout>
    <div>

        <ul class="nav nav-tabs mt-2 mx-auto">
            <li class="nav-item">
                <a class="nav-link" :class="{ active: activeTab === 'tab1' }" @click="activeTab = 'tab1'" href="#">HÓA ĐƠN
                    NỘI TRÚ</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" :class="{ active: activeTab === 'tab2' }" @click="activeTab = 'tab2'" href="#">HÓA ĐƠN
                    ĐIỆN NƯỚC</a>
            </li>
        </ul>
        <div class="col-lg-12 mx-auto mt-2">
            <div class="tab-content">
                <div v-show="activeTab === 'tab1'" class="tab-pane active">
                    <div>
                        <template slot="header">
                            <div class="row">

                                <div class="form-group mr-2">
                                    <select class="form-control" id="exampleCombobox" style="width: auto;">
                                        <option>Kì 1/2023</option>
                                        <option>Kì 2/2022</option>
                                        <option>Kì 1/2022</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <select class="form-control" id="exampleCombobox" style="width: auto;">
                                        <option>Đã đóng</option>
                                        <option>Chưa đóng</option>
                                    </select>
                                </div>
                            </div>
                            <p class="card-category"></p>
                        </template>
                        <table class="table table-sm table-hover ">
                            <thead class="thead-light">
                                <tr>
                                    <th><b>Id</b></th>
                                    <th><b>Họ và tên</b></th>
                                    <th><b>Phòng</b></th>
                                    <th><b>Kì</b></th>
                                    <th><b>Tổng tiền</b></th>
                                    <th><b>Trạng thái</b></th>
                                    <th>#</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(item, index) in paginatedItemsThuePhong" :key="item.id"
                                    @click="PayBillNoiTru(item)">
                                    <td>{{ index + 1 }}</td>
                                    <td>{{ item.hoten }}</td>
                                    <td>{{ item.tenphong }}</td>
                                    <td>{{ item.ki }}</td>
                                    <td>{{ item.tongtien.toLocaleString("vi-VN", { style: "currency", currency: "VND", }) }}
                                    </td>
                                    <td>
                                        <span v-if="item.status == 0" style="color: brown;"> Chưa đóng</span>
                                        <span v-if="item.status == 1" style="color:darkgreen ;"> Đã đóng</span>

                                    </td>
                                    <td>
                                        <!-- <button class="btn btn-primary" @click="showDetails = true">Xem chi tiết</button> -->

                                        <button class="btn btn-sm btn-primary">Thanh toán</button>

                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <!-- phân trang thuê phòng -->
                    <div class="pagination-container">
                        <div class="pagination">
                            <a @click="previousPageThuePhong" :disabled="currentPageThuePhong === 1">&laquo;</a>
                            <a v-for="page in totalPagesThuePhong" :key="page"
                                :class="{ active: page === currentPageThuePhong }" @click="goToPageThuePhong(page)">
                                {{ page }}
                            </a>
                            <a @click="nextPageThuePhong"
                                :disabled="currentPageThuePhong === totalPagesThuePhong">&raquo;</a>
                        </div>
                    </div>
                </div>
                <div v-show="activeTab === 'tab2'" class="tab-pane active">
                    <div>
                        <template slot="header">
                            <div class="row">
                                <p>(*) Giá chỉ số điện: 3.000 VNĐ/kWh - Giá chỉ số nước: 15.000/ m3</p>
                            </div>
                            <div class="row">
                                <div class="col-sm-10">
                                    <div class="form-group">
                                        <select class="form-control" id="exampleCombobox" style="width: auto;">
                                            <option>Đã đóng</option>
                                            <option>Chưa đóng</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="col-sm-2">

                                    <button class="btn btn-primary pr-2" @click="showSubform = true">Upload hóa đơn</button>

                                </div>
                            </div>
                            <p class="card-category"></p>
                        </template>
                        <table class="table table-sm table-hover ">
                            <thead class="thead-light">
                                <tr>
                                    <th><b>STT</b></th>
                                    <th><b>Phòng</b></th>
                                    <th><b>Từ ngày</b></th>
                                    <th><b>Đến ngày</b></th>
                                    <th><b>CS điện cũ</b></th>
                                    <th><b>CS điện mới</b></th>
                                    <th><b>Giá điện</b></th>
                                    <th><b>CS nước cũ</b></th>
                                    <th><b>CS nước mới</b></th>
                                    <th><b>Giá nước</b></th>
                                    <th><b>Tổng tiền</b></th>
                                    <th><b>Tình trạng</b></th>
                                    <th>#</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(item, index) in paginatedItemsDienNuoc" :key="item.id"
                                    @click="PayBillDienNuoc(item)">
                                    <td>{{ index + 1 }}</td>
                                    <td>{{ item.tenPhong }}</td>
                                    <td>{{ moment(item.hoaDonTienDienNuoc.startDate).format('DD/MM/yyyy ') }}</td>
                                    <td>{{ moment(item.hoaDonTienDienNuoc.endDate).format('DD/MM/yyyy ') }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.csDien1 }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.csDien2 }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.giadien }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.csNuoc1 }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.csNuoc2 }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.gianuoc }}</td>
                                    <td>{{ item.hoaDonTienDienNuoc.tongTien }}</td>
                                    <td>
                                        <span v-if="item.hoaDonTienDienNuoc.status == 0">Chưa đóng</span>
                                        <span v-if="item.hoaDonTienDienNuoc.status == 1">Đã đóng</span>
                                    </td>
                                    <td>
                                        <button class="btn btn-primary">Thanh toán</button>

                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <!-- phân trang tab điện nước -->
                    <div class="pagination-container">
                        <div class="pagination">
                            <a @click="previousPageDienNuoc" :disabled="currentPageDienNuoc === 1">&laquo;</a>
                            <a v-for="page in totalPagesDienNuoc" :key="page"
                                :class="{ active: page === currentPageDienNuoc }" @click="goToPageDienNuoc(page)">
                                {{ page }}
                            </a>
                            <a @click="nextPageDienNuoc" :disabled="currentPageDienNuoc === totalPagesDienNuoc">&raquo;</a>
                        </div>
                    </div>
                </div>


            </div>
        </div>

    </div>
</template>
  
<script>
import axios from 'axios'
import moment from 'moment';
export default {
    computed: {
        paginatedItemsDienNuoc() {
            const startIndex = (this.currentPageDienNuoc - 1) * this.itemsPerPage;
            const endIndex = startIndex + this.itemsPerPage;
            return this.dataDienNuoc.slice(startIndex, endIndex);
        },
        totalPagesDienNuoc() {
            return Math.ceil(this.dataDienNuoc.length / this.itemsPerPage);
        },
        paginatedItemsThuePhong() {
            const startIndex = (this.currentPageThuePhong - 1) * this.itemsPerPage;
            const endIndex = startIndex + this.itemsPerPage;
            return this.dataThuePhong.slice(startIndex, endIndex);
        },
        totalPagesThuePhong() {
            return Math.ceil(this.dataThuePhong.length / this.itemsPerPage);
        },
    },
    data() {
        return {
            moment,
            activeTab: 'tab1',
            showDetails: false,
            dataDienNuoc: [],
            dataThuePhong: [],
            showSubform: false,
            dataSubform: [],
            currentPageThuePhong: 1, // The current page number
            currentPageDienNuoc: 1, // The current page number
            itemsPerPage: 5, // The number of items to display per page
            id: 0
        }
    },
    methods: {
        getData() {
            const currentUrl = window.location.href; // lấy địa chỉ url hiện tại (url call back)

            if (currentUrl.length > 100) { // địa chỉ trả về sau khi thanh toán thành công
                axios.get('https://localhost:7252/api/VnPay/payment-callback', {
                    params: {
                        queryParams: currentUrl
                    }
                }).then(response => {
                    console.log(response.data);
                    if(response.data.loai == "1"){
                        this.UpdateBillNoiTru(response.data.idBill, response.data.status)
                    }else if(response.data.loai == "2"){
                        this.UpdateBillDienNuoc(response.data.idBill, response.data.status)
                    }
                 
                   window.location.href = "http://localhost:3000/pages/landing-pages/bill"
                }).catch(error => {
                    console.log(error);
                });
            }
            console.log(localStorage.getItem('phongid'))
            axios.get("https://localhost:7252/api/HoaDonTienDienNuocs/Phong/" + localStorage.getItem('phongid')).
                then(respone => {
                    this.dataDienNuoc = respone.data
                    console.log(this.dataDienNuoc)
                })
                .catch(error => {
                    console.log(error)
                });
            axios.get("https://localhost:7252/api/HopDongThuePhongs/SV/" + localStorage.getItem('userid')).
                then(respone => {
                    this.dataThuePhong = respone.data
                    console.log(this.dataThuePhong)
                })
                .catch(error => {
                    console.log(error)
                });
        },
        UpdateBillNoiTru(idbill, result) {
            axios.put('https://localhost:7252/api/HopDongThuePhongs/Payment', null, {
                params: {
                    id: idbill,
                    isSuccess: result
                }
            })
                .then(response => {
                    console.log(response.data);
                    this.getData()
                })
                .catch(error => {
                    console.log(error);
                });
        },
        UpdateBillDienNuoc(idbill, result) {
            axios.put('https://localhost:7252/api/HoaDonTienDienNuocs/Payment', null, {
                params: {
                    id: idbill,
                    isSuccess: result
                }
            })
                .then(response => {
                    console.log(response.data);
                    this.getData()
                })
                .catch(error => {
                    console.log(error);
                });
        },
        PayBillNoiTru(row) {  
            // 'https://localhost:7252/api/VnPay/create-payment-url' ,{orderType: row.idHopDong,amount: row.tongtien,orderDescription: row.ki, name:row.hoten}
            axios.post('https://localhost:7252/api/VnPay/create-payment-url', {
                orderType: '' + row.idHopDong,
                amount: row.tongtien,
                orderDescription: "1-" + row.idHopDong,
                name: '' + row.idHopDong
            })
                .then(response => {
                    console.log(response.data)
                    window.location.href = response.data;
                }).catch(error => {
                    console.log(error)
                })
        },
        PayBillDienNuoc(row) {
            axios.post('https://localhost:7252/api/VnPay/create-payment-url', {
                orderType: '' + row.hoaDonTienDienNuoc.idBill,
                amount: row.hoaDonTienDienNuoc.tongTien,
                orderDescription: "2-" + row.hoaDonTienDienNuoc.idBill ,
                name: '' + row.hoaDonTienDienNuoc.idBill
            })
                .then(response => {
                    console.log(response.data)
                      window.location.href = response.data;
                }).catch(error => {
                    console.log(error)
                })
        },
        handleFileChange(event) {
            this.selectedFile = event.target.files[0];
        },

        previousPageThuePhong() {
            if (this.currentPageThuePhong > 1) {
                this.currentPageThuePhong--;
            }
        },
        nextPageThuePhong() {
            if (this.currentPageThuePhong < this.totalPagesThuePhong) {
                this.currentPageThuePhong++;
            }
        },
        goToPageThuePhong(page) {
            this.currentPageThuePhong = page;
        },

        previousPageDienNuoc() {
            if (this.currentPageDienNuoc > 1) {
                this.currentPageDienNuoc--;
            }
        },
        nextPageDienNuoc() {
            if (this.currentPageDienNuoc < this.totalPagesDienNuoc) {
                this.currentPageDienNuoc++;
            }
        },
        goToPageDienNuoc(page) {
            this.currentPageDienNuoc = page;
        },
    },
    mounted() {
        this.getData()
    }
}


</script>
<style></style>