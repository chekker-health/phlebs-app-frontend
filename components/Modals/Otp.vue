<template>
  <div class="inner_ come-up">
    <div v-if="success">
      <AlertsSuccess :success-text="successText" />
    </div>
    <p class="title">
      Enter 6 digit recovery code
    </p>
    <p class="sub-title">
      We sent a verification link to your email, kindly click on the link to reset your password.
    </p>
    <p class="sub-title">
      Or enter the OTP sent.
    </p>
    <div class="form">
      <div v-if="error">
        <AlertsError :error-text="errorText" />
      </div>
      <p class="label">
        Enter code here
      </p>
      <PincodeInput
        v-model="code"
        :length="6"
        @input="error = false"
      />
      <button v-if="loading" class="bg_btn" disabled>
        <Loader class="come-down" />
      </button>
      <button v-else class="bg_btn" @click="submit()">
        Submit Code
      </button>
      <div class="bottom_sec">
        <p class="no_code">
          Didn't Recieve Code
        </p>
        <div class="resend" @click="resendOTP()">
          <p>Resend Code</p>
          <svg
            :class="spin ? 'spin-icon' : ''"
            width="14"
            height="14"
            viewBox="0 0 16 16"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path d="M7.99981 1.33352C8.88415 1.33642 9.75913 1.51468 10.5741 1.85797C11.3891 2.20127 12.1279 2.7028 12.7478 3.33352H10.6665C10.4897 3.33352 10.3201 3.40376 10.1951 3.52878C10.07 3.6538 9.99981 3.82337 9.99981 4.00018C9.99981 4.177 10.07 4.34656 10.1951 4.47159C10.3201 4.59661 10.4897 4.66685 10.6665 4.66685H13.4285C13.7568 4.66667 14.0715 4.53619 14.3037 4.30405C14.5358 4.07192 14.6663 3.75713 14.6665 3.42885V0.666851C14.6665 0.49004 14.5962 0.32047 14.4712 0.195446C14.3462 0.0704219 14.1766 0.000183976 13.9998 0.000183976C13.823 0.000183976 13.6534 0.0704219 13.5284 0.195446C13.4034 0.32047 13.3331 0.49004 13.3331 0.666851V2.05218C12.2313 1.05982 10.8749 0.39379 9.41588 0.128683C7.95688 -0.136424 6.45289 0.00985861 5.07233 0.551149C3.69177 1.09244 2.48915 2.00736 1.59915 3.19347C0.709148 4.37957 0.166904 5.79001 0.0331428 7.26685C0.0245317 7.35969 0.0353533 7.4533 0.0649181 7.54173C0.0944829 7.63015 0.142143 7.71145 0.20486 7.78044C0.267578 7.84943 0.343979 7.9046 0.429195 7.94243C0.514411 7.98027 0.606573 7.99993 0.699809 8.00018C0.862868 8.00226 1.02083 7.94341 1.14278 7.83515C1.26473 7.72688 1.34189 7.57701 1.35914 7.41485C1.50755 5.75535 2.27113 4.21132 3.49986 3.08608C4.7286 1.96083 6.33369 1.33571 7.99981 1.33352Z" fill="#00295D" />
            <path d="M15.3008 8.00005C15.1378 7.99798 14.9798 8.05683 14.8579 8.16509C14.7359 8.27335 14.6588 8.42323 14.6415 8.58539C14.5313 9.85421 14.0594 11.0648 13.2819 12.0735C12.5044 13.0822 11.4539 13.8468 10.2549 14.2764C9.05598 14.7061 7.75896 14.7828 6.51773 14.4975C5.2765 14.2121 4.14316 13.5768 3.25216 12.6667H5.3335C5.51031 12.6667 5.67988 12.5965 5.8049 12.4715C5.92992 12.3464 6.00016 12.1769 6.00016 12.0001C6.00016 11.8232 5.92992 11.6537 5.8049 11.5286C5.67988 11.4036 5.51031 11.3334 5.3335 11.3334H2.5715C2.4089 11.3333 2.24787 11.3653 2.09763 11.4274C1.94739 11.4896 1.81088 11.5808 1.6959 11.6958C1.58093 11.8108 1.48974 11.9473 1.42755 12.0975C1.36537 12.2478 1.33341 12.4088 1.3335 12.5714V15.3334C1.3335 15.5102 1.40373 15.6798 1.52876 15.8048C1.65378 15.9298 1.82335 16.0001 2.00016 16.0001C2.17697 16.0001 2.34654 15.9298 2.47157 15.8048C2.59659 15.6798 2.66683 15.5102 2.66683 15.3334V13.9481C3.76872 14.9404 5.1251 15.6064 6.5841 15.8716C8.04309 16.1367 9.54708 15.9904 10.9276 15.4491C12.3082 14.9078 13.5108 13.9929 14.4008 12.8068C15.2908 11.6207 15.8331 10.2102 15.9668 8.73339C15.9754 8.64055 15.9646 8.54693 15.9351 8.45851C15.9055 8.37008 15.8578 8.28879 15.7951 8.2198C15.7324 8.15081 15.656 8.09564 15.5708 8.0578C15.4856 8.01997 15.3934 8.0003 15.3002 8.00005H15.3008Z" fill="#00295D" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      spin: false,
      error: false,
      loading: false,
      success: false,
      successText: '',
      reference: '',
      code: '',
      email: ''
    }
  },
  methods: {
    resendOTP () {
      this.spin = true
      // console.log(this.email)
      this.email = this.$route.query.email
      this.$axios.$get(`auth/send/otp/via/sms/${this.email}`
      ).then((response) => {
        console.log(response)
        this.spin = false
        if (!response.error) {
          this.reference = response.data.reference
          this.success = true
          this.successText = 'OTP sent successfully'
          setTimeout(() => {
            this.success = false
          }, 3000)
        } else {
          this.error = true
          this.errorText = response.errorMsg
          setTimeout(() => {
            this.error = false
          }, 3000)
        }
      })
    },
    submit () {
      this.loading = true
      this.email = this.$route.query.email
      let reference = this.$route.query.ref
      if (this.reference === '') {
        reference = this.$route.query.ref
      } else {
        reference = this.reference
      }
      if (this.code.length < 6) {
        this.error = true
        this.loading = false
        this.errorText = 'Please fill up the OTP field'
        setTimeout(() => {
          this.error = false
        }, 3000)
      } else {
        this.$axios.$post(`/auth/verify/otp/${reference}`, {
          code: this.code,
          email: this.email
        }
        ).then((response) => {
          console.log(response)
          this.loading = false
          if (!response.error) {
            this.$emit('getCode', this.code)
            this.$emit('closeOtp')
          } else {
            this.error = true
            this.errorText = response.errorMsg
          }
        }).catch(() => {
          this.loading = false
        })
      }
    }
  }
}
</script>

<style scoped>

.inner_ {
  height: 100%;
  padding-top: 10vh;
}

.title {
  font-size: 20px;
  font-weight: 700;
  color: var(--primary-color);
}

.sub-title {
  color: black;
  margin-top: 10px;
}

.form {
  margin-top: 3rem;
}

.bg_btn {
  width: 100%;
  margin-top: 3.5vh;
}

.bottom_sec {
  padding-top: 3.5vh;
  display: flex;
  justify-content: space-between;
  width: 90%;
  margin: auto;
}

.no_code {
  color: rgba(0, 0, 0, 0.452);
}

.resend {
  display: flex;
  align-items: center;
  gap: 5px;
  cursor: pointer;
}

.resend p {
  color: var(--primary-color);
  font-weight: 700;
}

@media only screen and (max-width: 500px) {
  /* .inner_ {
    padding-top: 5vh;
  } */
  .title {
    font-size: 18px;
    margin-top: 1.5rem;
  }

  .sub-title {
    font-size: 13px;
  }

  .form {
    margin-top: 8vh;
  }
}
</style>
