<template>
  <div class="personal_ctn">
    <!-- <div v-if="dataLoader" class="inner">
      <LoadersAccount />
    </div> -->
    <div class="inner come-down">
      <div class="lhs">
        <div>
          <div class="user-image-container">
            <div class="user-image">
              <img :src="userImage === null ? altImage : userImage" alt="" @click="chooseFile">
            <!-- <img :src="require(`~${userImage === null ? altImage : userImage}`)" alt="" @click="chooseFile"> -->
            </div>
            <input
              id="formFileLg"
              ref="fileInput"
              class="select-image"
              type="file"
              name="image"
              accept="image/jpeg, image/png"
              @input="selectImgFile"
            >
            <div class="edit-icon">
              <Loader2 v-if="imageLoading" class="come-down" />
              <svg
                v-else
                width="16"
                height="16"
                viewBox="0 0 20 20"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <g clip-path="url(#clip0_262_5442)">
                  <path d="M15.8333 3.33333H15.41L13.59 0.973333C13.3554 0.671505 13.0553 0.427014 12.7122 0.258378C12.3692 0.0897429 11.9923 0.00138587 11.61 0L8.39 0C8.00775 0.00138587 7.63082 0.0897429 7.28778 0.258378C6.94473 0.427014 6.64456 0.671505 6.41 0.973333L4.59 3.33333H4.16667C3.062 3.33466 2.00296 3.77407 1.22185 4.55518C0.440735 5.3363 0.00132321 6.39534 0 7.5L0 15.8333C0.00132321 16.938 0.440735 17.997 1.22185 18.7782C2.00296 19.5593 3.062 19.9987 4.16667 20H15.8333C16.938 19.9987 17.997 19.5593 18.7782 18.7782C19.5593 17.997 19.9987 16.938 20 15.8333V7.5C19.9987 6.39534 19.5593 5.3363 18.7782 4.55518C17.997 3.77407 16.938 3.33466 15.8333 3.33333ZM7.73 1.99167C7.80806 1.89088 7.90808 1.80922 8.02244 1.7529C8.13681 1.69658 8.26252 1.66709 8.39 1.66667H11.61C11.7375 1.66721 11.8631 1.69676 11.9775 1.75307C12.0918 1.80938 12.1919 1.89097 12.27 1.99167L13.305 3.33333H6.695L7.73 1.99167ZM18.3333 15.8333C18.3333 16.4964 18.0699 17.1323 17.6011 17.6011C17.1323 18.0699 16.4964 18.3333 15.8333 18.3333H4.16667C3.50363 18.3333 2.86774 18.0699 2.3989 17.6011C1.93006 17.1323 1.66667 16.4964 1.66667 15.8333V7.5C1.66667 6.83696 1.93006 6.20107 2.3989 5.73223C2.86774 5.26339 3.50363 5 4.16667 5H15.8333C16.4964 5 17.1323 5.26339 17.6011 5.73223C18.0699 6.20107 18.3333 6.83696 18.3333 7.5V15.8333Z" fill="#00295D" />
                  <path d="M10 6.66666C9.0111 6.66666 8.0444 6.95991 7.22215 7.50932C6.39991 8.05872 5.75904 8.83962 5.3806 9.75325C5.00217 10.6669 4.90315 11.6722 5.09608 12.6421C5.289 13.612 5.76521 14.5029 6.46447 15.2022C7.16373 15.9015 8.05465 16.3777 9.02455 16.5706C9.99446 16.7635 10.9998 16.6645 11.9134 16.2861C12.827 15.9076 13.6079 15.2668 14.1573 14.4445C14.7068 13.6223 15 12.6556 15 11.6667C14.9987 10.341 14.4715 9.06999 13.5341 8.13259C12.5967 7.1952 11.3257 6.66799 10 6.66666ZM10 15C9.34073 15 8.69627 14.8045 8.1481 14.4382C7.59994 14.072 7.1727 13.5514 6.9204 12.9423C6.66811 12.3332 6.6021 11.663 6.73072 11.0164C6.85934 10.3698 7.1768 9.77582 7.64298 9.30964C8.10915 8.84347 8.7031 8.526 9.3497 8.39738C9.9963 8.26876 10.6665 8.33477 11.2756 8.58707C11.8847 8.83936 12.4053 9.2666 12.7716 9.81476C13.1378 10.3629 13.3333 11.0074 13.3333 11.6667C13.3333 12.5507 12.9821 13.3986 12.357 14.0237C11.7319 14.6488 10.8841 15 10 15Z" fill="#00295D" />
                </g>
                <defs>
                  <clipPath id="clip0_262_5442">
                    <rect width="20" height="20" fill="white" />
                  </clipPath>
                </defs>
              </svg>
            </div>
          </div>
          <p class="name">
            {{ userName }}
          </p>
        </div>
      </div>
      <div class="rhs">
        <div v-if="success">
          <AlertsSuccess :success-text="successText" />
        </div>
        <div v-if="error">
          <AlertsError :error-text="`Please Request Edit Access`" />
        </div>
        <div v-if="error2">
          <AlertsError :error-text="errorText2" />
        </div>
        <div class="rhs_in">
          <div>
            <div class="input_cont">
              <p class="label">
                Proficiency
              </p>
              <div class="form-select" @click="checkEdit()">
                <select v-model="proficiency" :disabled="inputDisabled">
                  <option value="null">
                    Select...
                  </option>
                  <option value="Nurse">
                    Nurse
                  </option>
                  <option value="Med Lab Scientists">
                    Med Lab Scientists
                  </option>
                  <option value="Science Lab Technician">
                    Science Lab Technician
                  </option>
                  <option value="Phlebotomist">
                    Phlebotomist
                  </option>
                  <option value="Others">
                    Others
                  </option>
                </select>
                <svg
                  v-if="editAccess"
                  width="12"
                  height="12"
                  viewBox="0 0 12 12"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0_76_1320)">
                    <path d="M11.4265 0.573977C11.0866 0.234575 10.6259 0.0439453 10.1455 0.0439453C9.66515 0.0439453 9.20443 0.234575 8.86451 0.573977L0.732508 8.70598C0.499633 8.93754 0.314989 9.21299 0.189257 9.51637C0.0635245 9.81976 -0.000798988 10.1451 7.49061e-06 10.4735V11.5C7.49061e-06 11.6326 0.0526859 11.7598 0.146454 11.8535C0.240222 11.9473 0.367399 12 0.500008 12H1.52651C1.85489 12.0009 2.18019 11.9367 2.48359 11.811C2.78698 11.6854 3.06243 11.5008 3.29401 11.268L11.4265 3.13548C11.7658 2.79557 11.9563 2.33496 11.9563 1.85473C11.9563 1.37449 11.7658 0.913879 11.4265 0.573977ZM2.58701 10.561C2.30501 10.8411 1.92399 10.9988 1.52651 11H1.00001V10.4735C0.999502 10.2764 1.03809 10.0812 1.11353 9.8992C1.18897 9.71717 1.29976 9.5519 1.43951 9.41298L7.61101 3.24148L8.76101 4.39148L2.58701 10.561ZM10.719 2.42848L9.46601 3.68198L8.31601 2.53448L9.56951 1.28098C9.64502 1.20563 9.73463 1.1459 9.83322 1.10518C9.93182 1.06447 10.0375 1.04357 10.1441 1.04369C10.2508 1.0438 10.3564 1.06493 10.4549 1.10586C10.5534 1.14679 10.6429 1.20672 10.7183 1.28223C10.7936 1.35774 10.8533 1.44735 10.8941 1.54594C10.9348 1.64454 10.9557 1.75019 10.9555 1.85686C10.9554 1.96353 10.9343 2.06914 10.8934 2.16764C10.8524 2.26615 10.7925 2.35563 10.717 2.43098L10.719 2.42848Z" fill="#00295D" />
                  </g>
                  <defs>
                    <clipPath id="clip0_76_1320">
                      <rect width="12" height="12" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
              </div>
            </div>
            <div class="input_cont">
              <p class="label">
                Gender
              </p>
              <div class="form-select" @click="checkEdit()">
                <select v-model="gender" :disabled="inputDisabled">
                  <option value="">
                    Select...
                  </option>
                  <option value="male">
                    Male
                  </option>
                  <option value="female">
                    Female
                  </option>
                </select>
                <svg
                  v-if="editAccess"
                  width="12"
                  height="12"
                  viewBox="0 0 12 12"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0_76_1320)">
                    <path d="M11.4265 0.573977C11.0866 0.234575 10.6259 0.0439453 10.1455 0.0439453C9.66515 0.0439453 9.20443 0.234575 8.86451 0.573977L0.732508 8.70598C0.499633 8.93754 0.314989 9.21299 0.189257 9.51637C0.0635245 9.81976 -0.000798988 10.1451 7.49061e-06 10.4735V11.5C7.49061e-06 11.6326 0.0526859 11.7598 0.146454 11.8535C0.240222 11.9473 0.367399 12 0.500008 12H1.52651C1.85489 12.0009 2.18019 11.9367 2.48359 11.811C2.78698 11.6854 3.06243 11.5008 3.29401 11.268L11.4265 3.13548C11.7658 2.79557 11.9563 2.33496 11.9563 1.85473C11.9563 1.37449 11.7658 0.913879 11.4265 0.573977ZM2.58701 10.561C2.30501 10.8411 1.92399 10.9988 1.52651 11H1.00001V10.4735C0.999502 10.2764 1.03809 10.0812 1.11353 9.8992C1.18897 9.71717 1.29976 9.5519 1.43951 9.41298L7.61101 3.24148L8.76101 4.39148L2.58701 10.561ZM10.719 2.42848L9.46601 3.68198L8.31601 2.53448L9.56951 1.28098C9.64502 1.20563 9.73463 1.1459 9.83322 1.10518C9.93182 1.06447 10.0375 1.04357 10.1441 1.04369C10.2508 1.0438 10.3564 1.06493 10.4549 1.10586C10.5534 1.14679 10.6429 1.20672 10.7183 1.28223C10.7936 1.35774 10.8533 1.44735 10.8941 1.54594C10.9348 1.64454 10.9557 1.75019 10.9555 1.85686C10.9554 1.96353 10.9343 2.06914 10.8934 2.16764C10.8524 2.26615 10.7925 2.35563 10.717 2.43098L10.719 2.42848Z" fill="#00295D" />
                  </g>
                  <defs>
                    <clipPath id="clip0_76_1320">
                      <rect width="12" height="12" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
              </div>
            </div>
          </div>
          <div>
            <div class="input_cont">
              <p class="label">
                Address
              </p>
              <div class="new_input" @click="checkEdit()">
                <input v-model="address" type="text" :disabled="inputDisabled" @focus="error2 = false">
                <svg
                  v-if="editAccess"
                  width="12"
                  height="12"
                  viewBox="0 0 12 12"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0_76_1320)">
                    <path d="M11.4265 0.573977C11.0866 0.234575 10.6259 0.0439453 10.1455 0.0439453C9.66515 0.0439453 9.20443 0.234575 8.86451 0.573977L0.732508 8.70598C0.499633 8.93754 0.314989 9.21299 0.189257 9.51637C0.0635245 9.81976 -0.000798988 10.1451 7.49061e-06 10.4735V11.5C7.49061e-06 11.6326 0.0526859 11.7598 0.146454 11.8535C0.240222 11.9473 0.367399 12 0.500008 12H1.52651C1.85489 12.0009 2.18019 11.9367 2.48359 11.811C2.78698 11.6854 3.06243 11.5008 3.29401 11.268L11.4265 3.13548C11.7658 2.79557 11.9563 2.33496 11.9563 1.85473C11.9563 1.37449 11.7658 0.913879 11.4265 0.573977ZM2.58701 10.561C2.30501 10.8411 1.92399 10.9988 1.52651 11H1.00001V10.4735C0.999502 10.2764 1.03809 10.0812 1.11353 9.8992C1.18897 9.71717 1.29976 9.5519 1.43951 9.41298L7.61101 3.24148L8.76101 4.39148L2.58701 10.561ZM10.719 2.42848L9.46601 3.68198L8.31601 2.53448L9.56951 1.28098C9.64502 1.20563 9.73463 1.1459 9.83322 1.10518C9.93182 1.06447 10.0375 1.04357 10.1441 1.04369C10.2508 1.0438 10.3564 1.06493 10.4549 1.10586C10.5534 1.14679 10.6429 1.20672 10.7183 1.28223C10.7936 1.35774 10.8533 1.44735 10.8941 1.54594C10.9348 1.64454 10.9557 1.75019 10.9555 1.85686C10.9554 1.96353 10.9343 2.06914 10.8934 2.16764C10.8524 2.26615 10.7925 2.35563 10.717 2.43098L10.719 2.42848Z" fill="#00295D" />
                  </g>
                  <defs>
                    <clipPath id="clip0_76_1320">
                      <rect width="12" height="12" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
              </div>
            </div>
            <div class="input_cont">
              <p class="label">
                Nearest Dropoff Location
              </p>
              <div class="new_input" @click="checkEdit()">
                <input v-model="dropoff" type="text" :disabled="inputDisabled">
                <svg
                  v-if="editAccess"
                  width="12"
                  height="12"
                  viewBox="0 0 12 12"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0_76_1320)">
                    <path d="M11.4265 0.573977C11.0866 0.234575 10.6259 0.0439453 10.1455 0.0439453C9.66515 0.0439453 9.20443 0.234575 8.86451 0.573977L0.732508 8.70598C0.499633 8.93754 0.314989 9.21299 0.189257 9.51637C0.0635245 9.81976 -0.000798988 10.1451 7.49061e-06 10.4735V11.5C7.49061e-06 11.6326 0.0526859 11.7598 0.146454 11.8535C0.240222 11.9473 0.367399 12 0.500008 12H1.52651C1.85489 12.0009 2.18019 11.9367 2.48359 11.811C2.78698 11.6854 3.06243 11.5008 3.29401 11.268L11.4265 3.13548C11.7658 2.79557 11.9563 2.33496 11.9563 1.85473C11.9563 1.37449 11.7658 0.913879 11.4265 0.573977ZM2.58701 10.561C2.30501 10.8411 1.92399 10.9988 1.52651 11H1.00001V10.4735C0.999502 10.2764 1.03809 10.0812 1.11353 9.8992C1.18897 9.71717 1.29976 9.5519 1.43951 9.41298L7.61101 3.24148L8.76101 4.39148L2.58701 10.561ZM10.719 2.42848L9.46601 3.68198L8.31601 2.53448L9.56951 1.28098C9.64502 1.20563 9.73463 1.1459 9.83322 1.10518C9.93182 1.06447 10.0375 1.04357 10.1441 1.04369C10.2508 1.0438 10.3564 1.06493 10.4549 1.10586C10.5534 1.14679 10.6429 1.20672 10.7183 1.28223C10.7936 1.35774 10.8533 1.44735 10.8941 1.54594C10.9348 1.64454 10.9557 1.75019 10.9555 1.85686C10.9554 1.96353 10.9343 2.06914 10.8934 2.16764C10.8524 2.26615 10.7925 2.35563 10.717 2.43098L10.719 2.42848Z" fill="#00295D" />
                  </g>
                  <defs>
                    <clipPath id="clip0_76_1320">
                      <rect width="12" height="12" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="bottom_btn slide-in-from-left">
      <button v-if="!updateLoading && editAccess" class="bg_btn" @click="updateChanges()">
        Update Changes
      </button>
      <button v-else-if="!updateLoading && !editAccess" class="bg_btn" @click="requestEdit = true">
        Request Edit Access
      </button>
      <button v-else class="bg_btn" disabled>
        <Loader class="come-down" />
      </button>
    </div>
    <ModalsConfirmationModal
      v-if="requestEdit"
      :modal-head="'Request Edit Access'"
      :modal-text="'Your personal information is a vital information for us. Making edit to these information would require  that you request permission from the admin.'"
      :bg-btn="'Request Edit Access'"
      :bg-loading="requestLoading"
      @close-modal="requestEdit = false"
      @bg-action="requestEditAccesss()"
    />
    <ModalsSuccessModal
      v-if="successModal"
      :modal-image="require('assets/gifs/96673-success.gif')"
      :modal-head="'Request Sent'"
      :modal-text="'Your Request has been sent and you will be contacted soon.'"
      :add-data-one="'Contact Support'"
      :add-data-two="'support@mychekker.com'"
      :bg-btn="'Close'"
      @close-modal="successModal = false"
      @bg-action="successModal = false"
    />
    <ModalsSuccessModal
      v-if="successModalSaved"
      :modal-image="require('assets/gifs/96673-success.gif')"
      :modal-head="'Update Saved'"
      :modal-text="'Update Changed successfully'"
      :bg-btn="'Close'"
      @close-modal="successModalSaved = false"
      @bg-action="successModalSaved = false"
    />
  </div>
</template>

<script>
import Cookies from 'js-cookie'
export default {
  props: {
    userData: {
      type: Object,
      default: () => {}
    },
    successText: {
      type: String,
      default: () => ''
    },
    success: {
      type: Boolean,
      default: () => false
    },
    dataLoader: {
      type: Boolean,
      default: () => true
    },
    errorText: {
      type: String,
      default: () => ''
    },
    error: {
      type: Boolean,
      default: () => false
    },
    imageLoading: {
      type: Boolean,
      default: () => false
    }
  },
  data () {
    return {
      proficiency: '',
      userName: '',
      address: '',
      gender: '',
      dropoff: '',
      error2: false,
      loading: false,
      errorText2: '',
      requestLoading: false,
      updateLoading: false,
      editAccess: false,
      requestEdit: false,
      successModal: false,
      successModalSaved: false,
      userImage: null,
      altImage: require('assets/images/no-image.png'),
      age: ''
    }
  },
  computed: {
    inputDisabled () {
      return this.editAccess === false
    }
  },
  watch: {
    userData: {
      immediate: true,
      handler (val) {
        // console.log(val)
        this.pushData()
      }
    }
  },
  created () {
    this.checkEditAccess()
  },
  methods: {
    checkEdit () {
      if (!this.editAccess) {
        this.error2 = true
        this.errorText2 = 'Please request edit access'
        setTimeout(() => {
          this.error2 = false
        }, 3000)
      }
    },
    pushData () {
      this.userName = `${this.userData.personal_information.firstname} ${this.userData.personal_information.lastname}`
      this.proficiency = this.userData.ProfessionalQualification.proficiency
      this.address = this.userData.personal_information.address
      this.gender = this.userData.personal_information.gender
      this.dropoff = this.userData.personal_information.dropoff
      this.userImage = this.userData.profiles.profile_pics
    },
    chooseFile () {
      this.$refs.fileInput.click()
    },
    selectImgFile (event) {
      const fileId = event.target.files[0]
      this.selectedImage = fileId
      // this.selectedImage = this.$refs.fileInput.value
      const fileInput = this.$refs.fileInput
      const imgFile = fileInput.files
      this.saveImage()

      if (imgFile && imgFile[0]) {
        const reader = new FileReader()
        reader.onload = (e) => {
          this.userImage = e.target.result
        }
        reader.readAsDataURL(imgFile[0])
        this.$emit('fileInput', imgFile[0])
      }
    },
    saveImage () {
      // console.log(this.selectedImage)
      // eslint-disable-next-line vue/no-mutating-props
      this.imageLoading = true
      this.$emit('saveImage', this.selectedImage)
    },
    requestEditAccesss () {
      this.requestLoading = true
      this.$axios.$get('/auth/personal/request/edit/access',
        {
          headers: {
            Authorization: `Bearer ${Cookies.get('token')}`
          }
        }
      ).then((response) => {
        this.requestLoading = false
        // console.log(response)
        this.requestEdit = false
        this.successModal = true
      }).catch((onrejected) => {
        // console.log(onrejected)
        this.requestLoading = false
      })
    },
    checkEditAccess () {
      this.loading = true
      this.$axios.$get('/auth/personal/is/access/given',
        {
          headers: {
            Authorization: `Bearer ${Cookies.get('token')}`
          }
        }
      ).then((response) => {
        // console.log(response)
        // this.pushData()
        this.editAccess = response.editAccess
        this.loading = false
      }).catch((onrejected) => {
        // console.log(onrejected)
        this.loading = false
      })
    },
    updateChanges () {
      this.updateLoading = true
      this.$axios.$patch('/auth/personal/update/changes',
        {
          proficiency: this.proficiency,
          address: this.address,
          gender: this.gender,
          dropoff: this.dropoff
        },
        {
          headers: {
            Authorization: `Bearer ${Cookies.get('token')}`
          }
        }
      ).then((response) => {
        this.updateLoading = false
        if (!response.error) {
          // console.log(response)
          this.successModalSaved = true
        } else {
          this.error2 = true
          this.errorText2 = response.errorMsg
        }
        this.editAccess = response.editAccess
      }).catch((onrejected) => {
        // console.log(onrejected)
        this.loading = false
      })
    }
  }
}
</script>

<style scoped>
.inner {
  display: flex;
  justify-content: space-between;
}

.lhs {
  width: 25%;
  padding: 4vh 0;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0px 4px 4px rgba(0, 41, 93, 0.09);
  border-radius: 4px;
}

.name {
  font-weight: 700;
  font-size: 16px;
  text-align: center;
}

.rhs {
  width: 72%;
  box-shadow: 0px 4px 4px rgba(0, 41, 93, 0.09);
  border-radius: 4px;
  padding: 2vh 4vw;
}

.rhs_in {
  display: flex;
  justify-content: space-between;
}

.rhs_in > div {
  flex-basis: 44%;
}

.user-image-container {
  margin-top: 20px;
  margin-bottom: 10px;
  position: relative;
  width: fit-content;
  height: fit-content;
}

.select-image {
  position: absolute;
  height: 10rem;
  width: 10rem;
  top: 0;
  z-index: 2;
  cursor: pointer;
  opacity: 0;
}

.user-image img {
  width: 6rem;
  height: 6rem;
  object-fit: cover;
  /* border: 10px solid rgba(15, 178, 243, 0.18); */
  border-radius: 100%;
  cursor: pointer;
}

.edit-icon {
  width: 34px;
  height: 34px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  background-color: #fff;
  position: absolute;
  right: 0%;
  top: 60%;
  cursor: pointer;
  box-shadow: 0px 4px 20px rgba(0, 41, 93, 0.1);
}

.input_cont {
  margin-bottom: 3vh;
}

.label {
  font-weight: 500;
  color: rgba(0, 0, 0, 0.5);
}

input {
  padding: 0;
}

.new_input {
  border-bottom: 1px solid rgba(0, 41, 93, 0.1);
  background-color: transparent;
  border-radius: 0;
}

.new_input svg {
  cursor: pointer;
}

.bottom_btn {
  display: flex;
  justify-content: flex-end;
  margin-top: 6vh;
}

.bg_btn {
  width: 11rem;
}

.form-select select {
  background-color: transparent;
  font-weight: 500;
  border-bottom: 1px solid rgba(0, 41, 93, 0.1);
  padding: 0;
  color: unset;
}

.new_input input:disabled,
.new_input input[disabled],
.form-select select:disabled,
.form-select select[disabled] {
  /* background-color: #F8F8F8; */
  cursor: not-allowed;
}

@media only screen and (max-width: 500px) {
  .inner {
    flex-direction: column;
  }

  .lhs {
    width: 100%;
    box-shadow: none;
  }

  .rhs {
    width: 100%;
    box-shadow: none;
  }

  .rhs_in {
    flex-direction: column;
  }

  .label {
    font-size: 13px;
  }

  .personal_input {
    font-size: 14px;
  }

  .bottom_btn {
    justify-content: center;
  }

  .bg_btn {
    width: 90%;
  }
}
</style>
