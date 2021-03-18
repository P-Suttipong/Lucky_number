<template>
  <q-page class="page2 row items-center justify-evenly q-pb-xl">
    <div>
      <div v-if="show" class="number column">
        <div v-for="i in 10" :key="i">
          <div class="row margin-left">
            <q-btn
              round
              :class="circleClass(number)"
              class="q-ma-sm"
              v-for="number in number[i - 1]"
              :key="number"
            >
              <div v-if="isActive(number)">
                <p class="text">{{ number }}</p>
              </div>
              <div v-else>
                <img class="image" src="~assets/bear.png" />
              </div>
            </q-btn>
          </div>
        </div>
        <!-- <div class="row">
          <button class="q-mx-sm" v-for="i in number0" :key="i">{{ i }}</button>
        </div>
        <div class="row q-mt-sm">
          <button class="q-mx-sm" v-for="i in number1" :key="i">{{ i }}</button>
        </div> -->
      </div>
      <div v-else>
        <q-spinner-cube color="brown" size="5.5em" />
      </div>
    </div>
  </q-page>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";
@Component
export default class Index extends Vue {
  private api = axios.create({
    baseURL: "https://us-central1-lucky-number-50139.cloudfunctions.net",
    headers: {
      crossdomain: true,
      "Access-Control-Allow-Origin": "*"
    }
  });
  private activeNumber: Array<string> = [];
  private show: boolean = false;

  private number: Array<Array<string>> = [
    ["00", "01", "02", "03", "04", "05", "06", "07", "08", "09"],
    ["10", "11", "12", "13", "14", "15", "16", "17", "18", "19"],
    ["20", "21", "22", "23", "24", "25", "26", "27", "28", "29"],
    ["30", "31", "32", "33", "34", "35", "36", "37", "38", "39"],
    ["40", "41", "42", "43", "44", "45", "46", "47", "48", "49"],
    ["50", "51", "52", "53", "54", "55", "56", "57", "58", "59"],
    ["60", "61", "62", "63", "64", "65", "66", "67", "68", "69"],
    ["70", "71", "72", "73", "74", "75", "76", "77", "78", "79"],
    ["80", "81", "82", "83", "84", "85", "86", "87", "88", "89"],
    ["90", "91", "92", "93", "94", "95", "96", "97", "98", "99"]
  ];
  // get circleClass(): string {
  //   return "unactive";
  // }
  public circleClass(number: string): string {
    if (this.activeNumber.some(x => x === number)) {
      return "circle-active";
    } else {
      if (parseInt(number) % 2 == 0) {
        return "circle-one";
      } else {
        return "circle-two";
      }
    }
  }

  public isActive(number: string): boolean {
    if (this.activeNumber.some(x => x === number)) {
      return false;
    } else {
      return true;
    }
  }

  public async fetchData() {
    await this.api.get("/getData").then((res: any) => {
      if (res) {
        // console.log(res);
        res.data.forEach((r: any) => {
          r.data.number.forEach((num: any) => {
            this.activeNumber.push(num);
            // console.log(num);
          });
        });
      }
    });
    this.show = true;
  }

  async created() {
    this.fetchData();
  }
}
</script>
<style scoped>
.page2 {
  background-color: #dfd3bd;
}
.number {
  margin-top: 20px;
  background-color: white;
  padding: 10px;
  border-radius: 50px;
  border: 2px dashed black;
}
.circle-one {
  background-color: #3e3e3e;
  width: 50px;
  height: 50px;
}
.circle-active {
  background-color: #534040;
  width: 50px;
  height: 50px;
}
.circle-two {
  background-color: #0c0c0c;
  width: 50px;
  height: 50px;
}
.image {
  width: 50px;
}

.text {
  color: white;
  margin-top: 13px;
  margin-left: 2px;
  font-size: 24px;
}

@media only screen and (max-width: 325px) {
  .number {
    background-color: white;
    padding: 10px;
    margin-left: 10px;
    margin-right: 10px;
    border-radius: 50px;
    border: 2px dashed black;
  }
  .margin-left {
    margin-left: 0px;
  }
  .text {
    color: white;
    margin-top: 2.5vw;
    margin-left: -3px;
    font-size: 5vw;
    font-weight: bold;
  }
  .image {
    margin-left: -4px;
    width: 12vw;
  }
}
@media only screen and (min-width: 326px) and (max-width: 400px) {
  .number {
    background-color: white;
    padding: 10px;
    margin-left: 10px;
    margin-right: 10px;
    border-radius: 50px;
    border: 2px dashed black;
  }
  .margin-left {
    margin-left: 10px;
  }
  .text {
    color: white;
    margin-top: 3vw;
    margin-left: 0px;
    font-size: 5vw;
    font-weight: bold;
  }
  .image {
    margin-left: 0px;
    width: 12vw;
  }
}

@media only screen and (min-width: 401px) and (max-width: 430px) {
  .number {
    background-color: white;
    padding: 10px;
    margin-left: 10px;
    margin-right: 10px;
    border-radius: 50px;
    border: 2px dashed black;
  }
  .margin-left {
    margin-left: 20px;
  }
  .text {
    color: white;
    margin-top: 3vw;
    margin-left: 0px;
    font-size: 5vw;
    font-weight: bold;
  }
}

@media only screen and (max-width: 415px) {
  .circle-one {
    background-color: #3e3e3e;
    width: 12vw;
    height: 12vw;
  }
  .circle-two {
    background-color: #0c0c0c;
    width: 12vw;
    height: 12vw;
  }
  .circle-active {
    background-color: #534040;
    width: 12vw;
    height: 12vw;
  }
}
</style>
