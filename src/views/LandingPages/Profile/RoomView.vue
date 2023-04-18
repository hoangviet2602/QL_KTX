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
  <BaseLayout title="" :breadcrumb="[{ label: 'THÔNG TIN PHÒNG CỦA BẠN', route: '#' }]">
  </BaseLayout>

  <section>
    <div class="container py-4">
      <form role="form" id="contact-form" method="post" autocomplete="off">
        <div class="row">
          <div class="col-lg-12 mx-0 d-flex justify-content-center flex-column ">
            <h4>Phòng của bạn</h4>
            <div class="card-body">
              <MaterialButton variant="gradient" color="secondary" class="w-auto me-2">Gia hạn</MaterialButton>
              <MaterialButton variant="gradient" color="secondary" class="w-auto me-2">Hủy</MaterialButton>
              <MaterialButton variant="gradient" color="secondary" class="w-auto me-2">Chuyển</MaterialButton>
              <div class="row">
                <div class="col-lg-12 mx-0">
                  <div class="col-lg-6 mx-auto bg-primary">

                  </div> 
                  <div class="col-lg-6 mx-auto bg-light">

                  </div> 
                </div>
              </div>








            </div>


          </div>


        </div>

      </form>
    </div>
  </section>
</template>


