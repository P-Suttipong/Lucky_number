<template>
  <q-layout view="hHh lpR fFf">
    <q-header class="page">
      <div class="row justify-center">
        <!-- <img class="q-mt-md logo" src="~assets/luckynumber.png" /> -->
        <p class="q-mt-lg title text_with_2px_border">เบอร์เงินสด 50</p>
      </div>
      <div class="row justify-center">
        <p class="description-1 text_with_2px_border">
          เบอร์เงินสดลุ้นสองตัวล่าง
        </p>
        <p class="q-ml-sm description-2 text_with_2px_border">ถูกรับ 3,500</p>
      </div>
      <div class="row q-mt-sm justify-center">
        <p class="description-3 text_with_2px_border">
          ** โอนก่อนหวยออกเท่านั้น ไม่โอนถูกไม่จ่ายนะคะ **
        </p>
      </div>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {};
  }
};
</script>
<style scoped>
.page {
  background: url("~assets/Number-background.png");
}
.logo {
  max-width: 300px;
}
.title {
  color: #0659eb;
  font-size: 64px;
  font-weight: bold;
  font-family: "palette";
  margin-bottom: -10px;
}
.description-1 {
  color: #c2ab81;
  font-size: 24px;
  font-weight: 900;
  font-family: "Mali", cursive;
}
.description-2 {
  color: #ce6137;
  margin-top: -12px;
  font-size: 36px;
  font-weight: 900;
  font-family: "Mali", cursive;
}
.description-3 {
  color: #ab6f57;
  margin-top: -12px;
  font-size: 16px;
  font-weight: 900;
  font-family: "Mali", cursive;
}

@media only screen and (max-width: 320px) {
}
@media only screen and (min-width: 321px) and (max-width: 415px) {
}

@media only screen and (max-width: 415px) {
  .title {
    color: #0659eb;
    font-size: 48px;
    font-weight: bold;
    font-family: "palette";
    margin-bottom: -10px;
    margin-top: 15px;
  }
  .description-1 {
    color: #c2ab81;
    font-size: 24px;
    font-weight: 900;
    font-family: "Mali", cursive;
  }
  .description-2 {
    color: #ce6137;
    margin-top: -12px;
    font-size: 36px;
    font-weight: 900;
    font-family: "Mali", cursive;
  }
  .description-3 {
    color: #ab6f57;
    margin-top: -12px;
    font-size: 13px;
    font-weight: 900;
    font-family: "Mali", cursive;
  }
}
</style>
