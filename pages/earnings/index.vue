<template>
  <div class="container">
    <div class="tab-ctn">
      <TabHeaders
        :tabs="['Earnings', 'Referrals']"
        padding-left="4px"
        :active-tab="activeTab"
        @set-active-tab="setActiveTab"
      />
    </div>
    <div v-if="activeTab === 'Earnings'" class="inner">
      <div v-if="warning" class="">
        <AlertsWarning :warning-head="'Instruction'" :warning-text="'Kindly Add a Primary Bank account bearing your name to allow easy withdrawal from your wallet'" />
      </div>
      <div v-if="loading" class="top_se">
        <LoadersEarnings />
      </div>
      <div v-else class="top_section">
        <div class="wallet_balance come-down">
          <p class="text">
            My Wallet Balance
          </p>
          <div class="top">
            <div class="text_side">
              <p v-if="hideBalance" class="orders">
                *******
              </p>
              <p v-else class="orders">
                {{ currency(balance ? balance : 0) }}
              </p>
            </div>
            <div class="icon">
              <svg
                v-if="hideBalance"
                class="pass_svg"
                width="26"
                height="26"
                viewBox="0 0 24 24"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                @click="showHide()"
              >
                <path d="M22.0828 11.3953C19.861 6.71484 16.5024 4.35938 12 4.35938C7.49533 4.35938 4.13908 6.71484 1.9172 11.3977C1.82808 11.5864 1.78186 11.7925 1.78186 12.0012C1.78186 12.2099 1.82808 12.416 1.9172 12.6047C4.13908 17.2852 7.49767 19.6406 12 19.6406C16.5047 19.6406 19.861 17.2852 22.0828 12.6023C22.2633 12.2227 22.2633 11.782 22.0828 11.3953ZM12 17.9531C8.21954 17.9531 5.45158 16.0359 3.49923 12C5.45158 7.96406 8.21954 6.04688 12 6.04688C15.7805 6.04688 18.5485 7.96406 20.5008 12C18.5508 16.0359 15.7828 17.9531 12 17.9531ZM11.9063 7.875C9.62814 7.875 7.78126 9.72188 7.78126 12C7.78126 14.2781 9.62814 16.125 11.9063 16.125C14.1844 16.125 16.0313 14.2781 16.0313 12C16.0313 9.72188 14.1844 7.875 11.9063 7.875ZM11.9063 14.625C10.4555 14.625 9.28126 13.4508 9.28126 12C9.28126 10.5492 10.4555 9.375 11.9063 9.375C13.357 9.375 14.5313 10.5492 14.5313 12C14.5313 13.4508 13.357 14.625 11.9063 14.625Z" fill="#fff" />
              </svg>
              <svg
                v-else
                class="pass_svg"
                width="26"
                height="26"
                viewBox="0 0 32 32"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                @click="showHide()"
              >
                <path d="M6 5.00012L26 27.0001" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M19.3634 19.6999C18.3822 20.5918 17.0868 21.0573 15.7623 20.9942C14.4378 20.9311 13.1926 20.3444 12.3006 19.3632C11.4086 18.3821 10.9429 17.0868 11.006 15.7622C11.069 14.4377 11.6555 13.1925 12.6366 12.3004" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M9.24931 8.57434C4.15315 11.155 2 16.0001 2 16.0001C2 16.0001 6 24.9992 16 24.9992C18.343 25.0178 20.6567 24.4782 22.7497 23.4248" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M26.0762 21.1376C28.8014 18.6967 30 16.0001 30 16.0001C30 16.0001 26 6.99917 16 6.99917C15.1339 6.99775 14.2692 7.06816 13.4147 7.20968" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                <path d="M16.9409 11.0886C18.0036 11.2927 18.9715 11.8358 19.6994 12.6365C20.4274 13.4373 20.876 14.4524 20.9781 15.5297" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
              </svg>
            </div>
          </div>
          <button :disabled="disabled" class="bg_btn" @click="$router.push('/earnings/withdraw')">
            <span>Withdraw</span>
            <svg width="36" height="35" viewBox="0 0 36 35" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M23.8614 19.8899L23.8542 13.7034C23.8526 13.1652 23.6381 12.6496 23.2576 12.269C22.877 11.8885 22.3614 11.674 21.8232 11.6724L15.6367 11.6652C15.3676 11.666 15.1098 11.7733 14.9195 11.9635C14.7293 12.1538 14.622 12.4116 14.6212 12.6807C14.6207 12.8152 14.6467 12.9484 14.6979 13.0727C14.7491 13.197 14.8244 13.31 14.9195 13.4051C15.0146 13.5002 15.1276 13.5755 15.2519 13.6267C15.3762 13.6779 15.5094 13.7039 15.6439 13.7034L20.3828 13.7034L12.4606 21.6256C12.2696 21.8166 12.1623 22.0757 12.1623 22.3458C12.1623 22.6159 12.2696 22.875 12.4606 23.066C12.6516 23.257 12.9107 23.3643 13.1808 23.3643C13.4509 23.3643 13.71 23.257 13.901 23.066L21.8232 15.1438L21.8232 19.8827C21.8223 20.153 21.9287 20.4126 22.1192 20.6044C22.3096 20.7962 22.5684 20.9044 22.8387 20.9054C23.109 20.9064 23.3686 20.7999 23.5604 20.6095C23.7522 20.419 23.8604 20.1602 23.8614 19.8899Z" fill="white" />
            </svg>
          </button>
        </div>
        <div class="acct_details come-down">
          <p class="text">
            Primary Bank Account
          </p>
          <div class="top">
            <div class="text_side">
              <p v-if="warning" class="orders">
                *******
              </p>
              <p v-else class="orders">
                {{ accountDetails ? accountDetails.account_number : 0 }}
              </p>
            </div>
            <div v-if="!warning" class="icon">
              <svg
                width="30"
                height="30"
                viewBox="0 0 40 40"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
                @click="editAcct()"
              >
                <rect width="40" height="40" rx="4" fill="#6F8CE4" />
                <g clip-path="url(#clip0_1841_9571)">
                  <path d="M12.7813 24.7469C12.2812 25.2469 12.0002 25.925 12 26.6322V28.0009H13.3687C14.0759 28.0007 14.754 27.7197 15.254 27.2196L24.1493 18.3242L21.6767 15.8516L12.7813 24.7469Z" fill="white" />
                  <path d="M27.43 12.5693C27.2677 12.4068 27.0749 12.2778 26.8627 12.1899C26.6505 12.1019 26.423 12.0566 26.1933 12.0566C25.9636 12.0566 25.7362 12.1019 25.524 12.1899C25.3118 12.2778 25.119 12.4068 24.9567 12.5693L22.6193 14.9073L25.092 17.3799L27.43 15.0426C27.5925 14.8803 27.7214 14.6875 27.8094 14.4753C27.8973 14.2631 27.9426 14.0356 27.9426 13.8059C27.9426 13.5762 27.8973 13.3488 27.8094 13.1366C27.7214 12.9244 27.5925 12.7316 27.43 12.5693Z" fill="white" />
                </g>
                <defs>
                  <clipPath id="clip0_1841_9571">
                    <rect width="16" height="16" fill="white" transform="translate(12 12)" />
                  </clipPath>
                </defs>
              </svg>
            </div>
          </div>
          <button
            v-if="warning"
            class="bg_btn add_btn"
            @click="addBankAccount = true"
          >
            <svg
              class="plus"
              width="16"
              height="15"
              viewBox="0 0 16 15"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path d="M6.65 14.955V8.835H0.62V6.195H6.65V0.224999H9.38V6.195H15.38V8.835H9.38V14.955H6.65Z" fill="white" />
            </svg>
            <span>Add Bank Account</span>
          </button>
          <div v-else class="details">
            <p class="text">
              {{ accountDetails.account_name }}
            </p>
            <p class="text">
              {{ accountDetails.bankofdeposit }}
            </p>
          </div>
        </div>
      </div>
      <div class="bottom_section">
        <div class="">
          <TablesEarningsTable />
        </div>
      </div>
    </div>
    <div v-if="activeTab === 'Referrals'" class="inner">
      <div class="referral_section">
        <p class="referral_head">
          Get More Bonus
        </p>
        <p class="referral_sub_head">
          Enjoy extra cash when you refer your friends and family to book tests using Chekker using your referral code.
        </p>
        <div class="referral_code" @click="copyCode()">
          <p v-if="code_copied" class="copied">
            Copied!
          </p>
          <p v-else ref="referral_code">
            {{ referral_code }}
          </p>
          <svg
            v-if="!code_copied"
            width="20"
            height="20"
            viewBox="0 0 20 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g clip-path="url(#clip0_1707_10415)">
              <path d="M10.8327 16.6667C11.9373 16.6654 12.9964 16.2259 13.7775 15.4448C14.5586 14.6637 14.998 13.6047 14.9993 12.5V5.20251C15.0006 4.76448 14.915 4.33055 14.7473 3.92586C14.5797 3.52118 14.3334 3.1538 14.0227 2.84501L12.1544 0.976681C11.8456 0.665993 11.4782 0.419684 11.0735 0.252031C10.6688 0.0843791 10.2349 -0.00128163 9.79685 1.44913e-05H5.83268C4.72802 0.00133771 3.66898 0.440749 2.88787 1.22186C2.10675 2.00298 1.66734 3.06202 1.66602 4.16668V12.5C1.66734 13.6047 2.10675 14.6637 2.88787 15.4448C3.66898 16.2259 4.72802 16.6654 5.83268 16.6667H10.8327ZM3.33268 12.5V4.16668C3.33268 3.50364 3.59607 2.86776 4.06492 2.39891C4.53376 1.93007 5.16964 1.66668 5.83268 1.66668C5.83268 1.66668 9.93185 1.67835 9.99935 1.68668V3.33335C9.99935 3.77538 10.1749 4.1993 10.4875 4.51186C10.8001 4.82442 11.224 5.00001 11.666 5.00001H13.3127C13.321 5.06751 13.3327 12.5 13.3327 12.5C13.3327 13.1631 13.0693 13.7989 12.6005 14.2678C12.1316 14.7366 11.4957 15 10.8327 15H5.83268C5.16964 15 4.53376 14.7366 4.06492 14.2678C3.59607 13.7989 3.33268 13.1631 3.33268 12.5ZM18.3327 6.66668V15.8333C18.3314 16.938 17.8919 17.9971 17.1108 18.7782C16.3297 19.5593 15.2707 19.9987 14.166 20H6.66602C6.445 20 6.23304 19.9122 6.07676 19.7559C5.92048 19.5997 5.83268 19.3877 5.83268 19.1667C5.83268 18.9457 5.92048 18.7337 6.07676 18.5774C6.23304 18.4211 6.445 18.3333 6.66602 18.3333H14.166C14.8291 18.3333 15.4649 18.07 15.9338 17.6011C16.4026 17.1323 16.666 16.4964 16.666 15.8333V6.66668C16.666 6.44567 16.7538 6.23371 16.9101 6.07743C17.0664 5.92115 17.2783 5.83335 17.4993 5.83335C17.7204 5.83335 17.9323 5.92115 18.0886 6.07743C18.2449 6.23371 18.3327 6.44567 18.3327 6.66668Z" fill="#00295D" fill-opacity="0.5" />
            </g>
            <defs>
              <clipPath id="clip0_1707_10415">
                <rect width="20" height="20" fill="white" />
              </clipPath>
            </defs>
          </svg>
        </div>
        <div class="referral_bottom_btn">
          <button class="referral_btn bg_btn" @click="shareWithFriends = true">
            Share Your Code
          </button>
        </div>
        <p class="referral_bottom_text" @click="$router.push('/earnings/referral-history')">
          VIEW MY REFERRAL PERFORMANCE
        </p>
      </div>
    </div>
    <ModalsAddBankAccount
      v-if="addBankAccount"
      @close-modal="addBankAccount = false"
      @bg-action="addBank()"
    />
    <ModalsSuccessModal
      v-if="successModal"
      :modal-image="require('assets/gifs/Successful  - Completed.gif')"
      :modal-head="'Your Primary Account has been added succesfully'"
      :modal-text="'To modify subsequetly, kindly contact support'"
      :bg-btn="'Close'"
      @close-modal="$router.app.refresh()"
      @bg-action="$router.app.refresh()"
    />
    <ModalsSuccessModal
      v-if="setPin"
      :modal-image="require('assets/gifs/Pin.gif')"
      :modal-head="'You???ve not setup you Withdrawal Pin'"
      :modal-text="'This pin would be required for you to complete your withdrawal'"
      :bg-btn="'Set Pin'"
      @bg-action="$router.push('/my-account?type=security')"
    />
    <ModalsShareWithFriends
      v-if="shareWithFriends"
      :referral-code="referral_code"
      @close-modal="shareWithFriends = false"
    />
    <ModalsContactSupport
      v-if="infoBox"
      :bg-btn="'Close'"
      @close-modal="infoBox = false"
      @bg-action="infoBox = false"
    />
  </div>
</template>

<script>
import Cookies from 'js-cookie'
import functions from '@/utils/functions'
export default {
  layout: 'MainLayout',
  data () {
    return {
      currency: functions.formatCurrency,
      // warning: true,
      activeTab: 'Earnings',
      referral_code: '',
      code_copied: false,
      acctApproved: true,
      infoBox: false,
      loading: false,
      shareWithFriends: false,
      hideBalance: true,
      setPin: false,
      isBankAccountAdded: true,
      addBankAccount: false,
      successModal: false,
      accountDetails: {},
      balance: ''
    }
  },
  computed: {
    disabled () {
      return this.warning === true
    },
    warning () {
      return (!this.isBankAccountAdded || !this.acctApproved)
    }
  },
  created () {
    this.$store.commit('setPageName', this.activeTab)
    this.getUserDetails()
  },
  methods: {
    getUserDetails () {
      this.loading = true
      this.$axios.$get('/auth/all/registration/information', {
        headers: {
          Authorization: `Bearer ${Cookies.get('token')}`
        }
      }).then((response) => {
        // console.log(response)
        this.acctApproved = response.data.reg_details.approved
        if (!this.acctApproved) {
          this.warning = true
          this.loading = false
        } else {
          this.checkWithdrawalPin()
          this.checkIfBankAdded()
          this.getWalletBalace()
          this.getPrimaryAccount()
          this.getReferralCode()
        }
      })
    },
    setActiveTab (tab) {
      this.activeTab = tab
      this.$store.commit('setPageName', tab)
      if (this.activeTab === 'Earnings') {
        this.checkWithdrawalPin()
        this.checkIfBankAdded()
        this.getWalletBalace()
        this.getPrimaryAccount()
      } else if (this.activeTab === 'Referrals') {
        // this.getDismissedOrders()
      }
    },
    editAcct () {
      this.infoBox = !this.infoBox
      setTimeout(() => {
        this.infoBox = false
      }, 7000)
    },
    copyCode () {
      navigator.clipboard.writeText(this.referral_code)
      this.code_copied = true
      setTimeout(() => {
        this.code_copied = false
      }, 3000)
    },
    showHide () {
      this.hideBalance = !this.hideBalance
    },
    addBank () {
      this.addBankAccount = false
      this.successModal = true
    },
    checkWithdrawalPin () {
      this.loading = true
      this.$axios.$get('/earning/check/if/pin/setup', {
        headers: {
          Authorization: `Bearer ${Cookies.get('token')}`
        }
      }).then((response) => {
        // this.loading = false
        // console.log(response)
        if (!response.pin) {
          this.setPin = true
        } else {
          this.setPin = false
        }
      })
    },
    checkIfBankAdded () {
      // this.loading = true
      this.$axios.$get('/earning/is/primary/bank/added', {
        headers: {
          Authorization: `Bearer ${Cookies.get('token')}`
        }
      }).then((response) => {
        // this.loading = false
        // console.log(response)
        this.isBankAccountAdded = response.isBankAccountAdded
      })
    },
    getWalletBalace () {
      // this.loading = true
      this.$axios.$get('/auth/wallet/balance', {
        headers: {
          Authorization: `Bearer ${Cookies.get('token')}`
        }
      }).then((response) => {
        // this.loading = false
        // console.log(response)
        this.balance = response.wallet_amount
      })
    },
    getPrimaryAccount () {
      // this.loading = true
      this.$axios.$get('/earning/get/primary/account', {
        headers: {
          Authorization: `Bearer ${Cookies.get('token')}`
        }
      }).then((response) => {
        this.loading = false
        // console.log(response)
        this.accountDetails = response.data
      })
    },
    getReferralCode () {
      // this.loading = true
      this.$axios.$get('/auth/refferal/code', {
        headers: {
          Authorization: `Bearer ${Cookies.get('token')}`
        }
      }).then((response) => {
        // this.loading = false
        // console.log(response)
        this.referral_code = response.refferral_code
      })
    }
  }
}
</script>

<style scoped>
.container {
  padding: 2vh 3vw 5vh;
}

.tab-ctn {
  margin-bottom: 30px;
}

.inner {
  width: 95%;
}

.top_section {
  display: flex;
  width: 60%;
  justify-content: space-between;
}

.wallet_balance {
  width: 47%;
  background-color: #00295D;
  padding: 3vh 2vw;
  border-radius: 10px;
}

.acct_details {
  width: 47%;
  background-color: #2F374F;
  padding: 3vh 2vw;
  border-radius: 10px;
}

.top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.text {
  font-weight: 500;
  margin-bottom: 10px;
  color: rgba(255, 255, 255, 0.500);
}

.orders {
  font-size: 26px;
  font-weight: 700;
  color: #fff;
}

.row_details {
  z-index: 2;
  position: absolute;
  top: 50px;
  left: 20%;
  background-color: #fff;
  width: 20rem;
  height: fit-content;
  padding: 20px;
  box-shadow: 0px 4px 4px rgba(0, 41, 93, 0.09);
  border-radius: 10px;
}

.title_top {
  display: flex;
  align-items: center;
}

.details_head {
  margin-left: 10px;
  font-weight: 700;
}

.to {
  color: rgba(0, 0, 0, 0.5);
  margin-top: 20px;
  font-weight: 500;
}

.acct_det {
  margin-top: 10px;
}

.acct_info {
  margin-top: 5px;
  font-weight: 500;
}

.bg_btn {
  margin-top: 2vh;
  background-color: #6F8CE4;
  display: flex;
  align-items: center;
  justify-content: center;
  /* gap: 10px; */
  width: 10rem;
}

.bg_btn span {
  color: #fff;
  font-weight: 500;
  margin-right: 10px;
}

.add_btn {
  background-color: #2A7FF3;
  width: 12rem;
}

.add_btn span{
  margin-left: 10px;
  margin-right: 0;
}

.pass_svg {
  cursor: pointer;
}

.icon {
  position: relative;
}

.icon svg {
  cursor: pointer;
}

.details {
  margin-top: 10px;
}

.details .text {
  margin-top: 10px;
  margin-bottom: 0;
}

button:disabled,
button[disabled] {
  background-color: #cacaca;
  color: #929292;
  cursor: not-allowed;
  opacity: 0.7;
}

.bottom_section {
  margin-top: 5vh;
}

.table_title {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 2.5vh;
}

.add_btn svg {
  width: 15px;
  height: 15px;
}

/* REFERRAL */

.referral_section {
  width: 50%;
  margin: auto;
  margin-top: 40px;
}

.referral_head {
  font-weight: 700;
  font-size: 18px;
  color: #00295D;
  text-align: center;
}

.referral_sub_head {
  text-align: center;
  color: rgba(0, 0, 0, 0.7);
  margin-top: 10px;
}

.referral_code {
  display: flex;
  justify-content: center;
  align-items: center;
  width: fit-content;
  margin: auto;
  margin-top: 30px;
  cursor: pointer;
}

.referral_code p {
  margin-right: 5px;
  font-weight: 700;
  font-size: 22px;
  color: #00295D;
}

.referral_bottom_btn {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.referral_btn {
  background-color: #00295D;
}

.referral_bottom_text {
  text-align: center;
  color: #00295D;
  font-weight: 600;
  margin-top: 60px;
  cursor: pointer;
}

@media only screen and (max-width: 500px) {
  .container {
    padding-bottom: 5vh;
  }
  .inner {
    width: 100%;
  }
  .wallet_balance {
    width: 60%;
    padding-bottom: 2vh;
  }

  .acct_details {
    width: 60%;
    padding-bottom: 2vh;
  }

  .row_details {
    left: unset;
    right: 0;
  }

  .today_order {
    width: 38%;
    padding-left: 3vw;
    padding-bottom: 2vh;
  }

  /* .orders {
    font-size: 16px;
  } */

  .top .icon svg {
    width: 36px;
    height: 36px;
  }

  .top_section {
    flex-direction: column;
    width: 100%;
  }

  .wallet_balance {
    width: 100%;
    padding: 5vw;
  }

  .acct_details {
    width: 100%;
    padding: 5vw;
    margin-top: 15px;
  }

  .trans_btn {
    height: 45px;
  }

  .bg_btn {
    height: 45px;
  }

  .bg_btn svg {
    width: 24px;
    height: 24px;
  }

  .add_btn svg {
    width: 15px;
    height: 15px;
  }

  /* REFERRAL */

  .referral_section {
    width: 95%;
  }
}
</style>
