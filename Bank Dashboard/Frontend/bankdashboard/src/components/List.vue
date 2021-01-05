<template>
  <div class="d-flex">
    <div class="ml-n5" @click="scrollLeft" id="left_arrow">
      <v-img class="mt-16" src="../assets/arrow_backward.svg" />
    </div>
    <v-row class="list-container overflow-y-auto ml-2 mr-2" ref="accountsList" id="accounts_list">
      <v-col>
        <div class="d-flex mt-3">
          <div v-for="(account, i) in accountData" :key="i">
            <div id="details">
              <div class="d-flex mr-16">
                <v-card height="100" width="200" class="mr-2">
                  <v-img
                    :src="'http://localhost:3000/images/' + account.image"
                    contain
                  />
                </v-card>
                <v-btn class="mt-16 text-capitalize" :small="true">
                  <v-icon class="ml-n2 mr-2" :small="true">
                    mdi-arrow-right-drop-circle
                  </v-icon>
                  Apply now
                </v-btn>
              </div>
              <savings-details :type="account.type" :roi="account.ROI" :transaction="account.transaction"/>
              <fixed-deposits-details :type="account.type" :roi="account.ROI" :amount="account.amount" :term="account.term"/>
            </div>
          </div>
        </div>
      </v-col>
    </v-row>
    <div class="mr-5" @click="scrollRight" id="right_arrow">
      <v-img class="mt-16" src="../assets/arrow_forward.svg" />
    </div>
  </div>
</template>

<script>
import FixedDepositsDetails from './FixedDepositsDetails.vue';
import SavingsDetails from './SavingsDetails.vue';
export default {
  components: { SavingsDetails, FixedDepositsDetails },
    props: ['accountData'],
    methods: {
        scrollLeft() {
            const wrapper = this.$refs.accountsList;
            let scrollAmount = 400;
            var slideTimer = setInterval(function() {
                wrapper.scrollLeft -= 10;
                scrollAmount -= 10;
                if (scrollAmount <= 0) {
                window.clearInterval(slideTimer);
                }
            }, 15);
        },
        scrollRight() {
            const wrapper = this.$refs.accountsList;
            let scrollAmount = 0;
            var slideTimer = setInterval(function() {
                wrapper.scrollLeft += 10;
                scrollAmount += 10;
                if (scrollAmount >= 400) {
                window.clearInterval(slideTimer);
                }
            }, 15);
        },
        checkTotalAccounts() {
            const acc = Object.keys(this.accountData).length;
            if (acc <= 3) {
                document.querySelector("#left_arrow").style.display = "none";
                document.querySelector("#right_arrow").style.display = "none";
            }
        }
    },
    updated() {
        this.checkTotalAccounts();
    }
};
</script>

<style>
.list-container::-webkit-scrollbar {
  display: none;
  scroll-behavior: smooth;
}
</style>