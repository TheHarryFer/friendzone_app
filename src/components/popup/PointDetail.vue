<template>
  <div>
    <div id="wait-box" class="popup">
      <div class="popup-section section">
        <div>
          <div id="top-section" class="popup-form">
            <!-- <h1 class="header_title">WAIT FOR APPROVAL</h1> -->
            <h1 class="header_title">
              POINT
            </h1>

            <div id="yellow-box" class="section">
              <div>
                <div class="section">
                  <img id="coin-logo" src="@/assets/icon/coin.png" />
                  <h1 id="point">{{ point.point }}</h1>
                </div>
                <h1 id="your-balance">Your Balance</h1>
              </div>
            </div>

            <img
              @click="pointClick()"
              style="cursor: pointer"
              class="close"
              src="@/assets/icon/icons8-multiply-96.png"
            />
          </div>
          <div id="bottom-section" class="popup-form">
            <div id="menu">
              <h1 @click="clickEventDetail()" class="menu-text selected">
                Point Log
              </h1>
            </div>
            <hr id="bar" />

            <div v-if="pointLogList.length" id="transaction-box">
              <div v-for="(pointLog, i) in pointLogList" :key="i">
                <div id="transaction">
                  <div class="transaction-flex">
                    <h1 class="transaction-text transaction-title black-color">
                      {{ pointLog.title }}
                    </h1>
                    <h1
                      v-if="pointLog.point == 0"
                      class="transaction-text gray-color"
                    >
                      {{ pointLog.point }} P
                    </h1>
                    <h1
                      v-if="pointLog.point > 0"
                      class="transaction-text green-color"
                    >
                      +{{ pointLog.point }} P
                    </h1>
                    <h1
                      v-if="pointLog.point < 0"
                      class="transaction-text red-color"
                    >
                      {{ pointLog.point }} P
                    </h1>
                  </div>
                  <div class="transaction-flex">
                    <h1 class="transaction-info">{{ pointLog.description }}</h1>
                    <h1 class="transaction-info">{{ pointLog.date }}</h1>
                  </div>
                </div>
              </div>
            </div>
            <div v-else><NoInformation /></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PointTransactionService from "../../services/pointTransaction.service";
import NoInformation from "@/components/NoInformation.vue";

export default {
  data() {
    return {
      point: "",
      pointLogList: []
    };
  },
  components: {
    NoInformation
  },
  created() {
    PointTransactionService.getPoint().then((res) => {
      if (res) {
        this.point = res;
      }
    });
    PointTransactionService.getPointLog().then((res) => {
      if (res) {
        this.pointLogList = res;
      }
    });
  },
  methods: {
    pointClick() {
      this.$emit("point", false);
    }
  }
};
</script>

<style scoped>
#yellow-box {
  border: 2px solid #ffc449;
  border-radius: 9px;
  padding: 30px 130px;
}

#coin-logo {
  width: 35px;
  height: 35px;
}

#top-section {
  padding-bottom: 25px;
}

#bottom-section {
  margin-top: 20px;
  padding-top: 20px;
  padding-bottom: 20px;
}

#point {
  font-size: 4em;
  color: #444444;
  font-weight: 500;
  margin: 0px 0px 0px 10px;
}

#your-balance {
  font-size: 1.75em;
  color: #a0a0a0;
  text-transform: uppercase;
  font-weight: 400;
  text-align: center;
  margin: 10px 0px 0px 0px;
}

#menu {
  display: flex;
}

div::-webkit-scrollbar {
  height: 5px;
  width: 5px;
}

#transaction {
  margin-bottom: 15px;
}

#transaction-box {
  margin-top: 15px;
  height: 270px;
  overflow-y: auto;
  padding: 0px 15px 0px 0px;
}

.transaction-flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.transaction-text {
  font-size: 1.75em;
  margin: 0px;
  font-weight: 500;
}

.transaction-title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  width: 240px;
}

.transaction-info {
  font-size: 1.5em;
  margin: 0px;
  font-weight: 500;
  color: #a0a0a0;
}

#bar {
  height: 0.1px;
  border-width: 0;
  color: #a0a0a0;
  background-color: #a0a0a0;
  margin-top: -15px;
}
.menu-text {
  font-size: 2.25em;
  font-weight: 500;
  padding-right: 19px;
  margin-top: 5px;
  padding-bottom: 7px;
  color: #444444;
  cursor: pointer;
}

.selected {
  font-weight: 600;
  border-bottom: 5px solid #fe8864;
}

@media screen and (max-width: 1024px) {
  .popup-form {
    margin: 50px 0px 20px 0px;
  }
}

@media screen and (max-width: 690px) {
  #yellow-box {
    padding: 30px 100px;
  }

  .transaction-title {
    width: 180px;
  }

  #point {
    font-size: 3em;
  }

  #coin-logo {
    width: 25px;
    height: 25px;
  }
}

@media screen and (max-width: 490px) {
  .popup-form {
    padding-right: 30px !important;
    padding-left: 30px !important;
  }

  #transaction-box {
    width: 240px;
  }

  .transaction-text {
    font-size: 1.5em;
  }

  .transaction-info {
    font-size: 1.3em;
  }

  .transaction-title {
    width: 150px;
  }

  #yellow-box {
    padding: 20px 0px;
  }
}
</style>
