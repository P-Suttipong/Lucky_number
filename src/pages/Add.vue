<template>
  <div>
    <div class="q-mt-lg row justify-center">
      <q-btn @click="confirm = true" class="add-btn">เพิ่มข้อมูล</q-btn>
    </div>
    <div class="q-mt-lg column d-flex flex-center">
      <div
        class="row justify-center"
        v-for="(item, index) in data"
        :key="index"
      >
        <div class="q-ml-xs data-area row justify-between">
          <p class="data col-3">{{ item.data.name }}</p>
          <p class="data col-7">{{ item.data.number }}</p>
          <p
            @click="updateData(item.id, item.data.name, item.data.number)"
            class="update-btn q-mr-xs data col-1"
          >
            <i class="fas fa-pen"></i>
          </p>
        </div>
      </div>
    </div>
    <q-dialog v-model="confirm" persistent>
      <q-card>
        <q-card-section class="row justify-center">
          <p v-if="!loading" class="title">เพิ่มข้อมูล</p>
          <q-spinner-cube v-else color="brown" size="2em" />
        </q-card-section>

        <q-card-section>
          <div class="row justify-center">
            <div class="column">
              <q-input class="input" outlined v-model="name" label="ชื่อ" />
              <q-input class="input" outlined v-model="number" label="เลข" />
              <q-input
                type="password"
                class="input"
                outlined
                v-model="password"
                label="รหัส"
              />
            </div>
          </div>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn label="ยกเลิก" color="negative" v-close-popup />
          <q-btn
            @click="addData(name, number)"
            label="เพิ่ม"
            color="positive"
          />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="confirmUpdate" persistent>
      <q-card>
        <q-card-section class="row justify-center">
          <p v-if="!loading" class="title">อัพเดทข้อมูล</p>
          <q-spinner-cube v-else color="brown" size="2em" />
        </q-card-section>

        <q-card-section>
          <div class="row justify-center">
            <div class="column">
              <q-input
                class="input"
                outlined
                v-model="updatename"
                label="ชื่อ"
              />
              <q-input
                class="input"
                outlined
                v-model="updatenumber"
                label="เลข"
              />
              <q-input
                type="password"
                class="input"
                outlined
                v-model="updatepassword"
                label="รหัส"
              />
            </div>
          </div>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn label="ยกเลิก" color="negative" v-close-popup />
          <q-btn @click="confirmUpdateData()" label="เพิ่ม" color="positive" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";
@Component
export default class Add extends Vue {
  private number: any = [];
  private name: string = "";
  private updatenumber: any = [];
  private updatename: string = "";
  private ref: string = "";
  private confirm: boolean = false;
  private confirmUpdate: boolean = false;
  private data: any = "";
  private password: any = "";
  private updatepassword: any = "";
  private loading: boolean = false;

  private api = axios.create({
    baseURL: "https://us-central1-lucky-number-50139.cloudfunctions.net",
    headers: {
      crossdomain: true,
      "Access-Control-Allow-Origin": "*"
    }
  });

  public async fetchData() {
    await this.api.get("/getData").then((res: any) => {
      if (res) {
        // console.log(res);
        this.data = res.data;
      }
    });
  }

  public async addData(name: any, number: any) {
    var numArray = await number.split(",");
    // console.log(numArray);
    this.loading = true;
    if (this.password === "081243") {
      await this.api
        .post("/addData", {
          name: name,
          number: numArray
        })
        .then((res: any) => {
        //   console.log(res);
        });
      this.name = "";
      this.password = "";
      this.number = [];
      this.fetchData();
      this.loading = false;
      this.confirm = false;
    } else {
      this.password = "";
      this.loading = false;
      console.log("wrong password");
    }
  }

  public async updateData(id: any, name: any, number: any) {
    // console.log(id, name, number);
    this.updatename = name;
    this.updatenumber = number.toString();
    this.ref = id;
    this.confirmUpdate = true;
  }

  public async confirmUpdateData() {
    // console.log(this.updatenumber);
    var numArray = await this.updatenumber.split(",");
    // console.log(numArray);
    this.loading = true;
    if (this.updatepassword === "081243") {
      await this.api
        .put("/updateData", {
          id: this.ref,
          name: this.updatename,
          number: numArray
        })
        .then((res: any) => {
        //   console.log(res);
        });
      this.updatename = "";
      this.updatepassword = "";
      this.ref = "";
      this.updatenumber = [];
      this.fetchData();
      this.loading = false;
      this.confirmUpdate = false;
    } else {
      console.log("wrong password");
      this.loading = false;
      this.updatepassword = "";
    }
  }

  mounted() {
    this.fetchData();
  }
}
</script>
<style scoped>
.title {
  color: #534040;
  font-size: 30px;
  font-weight: bold;
  font-family: "palette";
}
.input {
  width: 300px;
  margin-bottom: 20px;
}
.add-btn {
  font-size: 16px;
  font-weight: bold;
  font-family: "Sarabun", sans-serif;
  background-color: #534040;
  color: white;
}
.data {
  color: #303030;
  font-size: 20px;
  font-weight: bold;
  font-family: "Sarabun", sans-serif;
}
.data-area {
  width: 500px;
}
.update-btn {
  color: #534040;
}
.update-btn:hover {
  color: #ce6137;
  cursor: pointer;
}
@media only screen and (max-width: 415px) {
  .input {
    width: 80vw;
    margin-bottom: 20px;
  }
  .data-area {
    width: 100vw;
  }
}
</style>
