<template>
  <div>
    <TablesLoader v-if="tableLoader" />
    <div v-else>
      <div v-if="tableData.length">
        <div class="mobile_no_show table-container come-down">
          <table>
            <tr class="table-header">
              <th class="date">
                Collection Date
              </th>
              <th class="time">
                Collection Time
              </th>
              <th class="address">
                <div class="address_ctn">
                  <svg width="18" height="20" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <g clip-path="url(#clip0_866_4032)">
                      <path d="M8.73441 0C6.80464 0.00242633 4.95451 0.881179 3.58996 2.44346C2.22541 4.00573 1.45787 6.12394 1.45575 8.33333C1.45575 12.735 7.56982 18.7775 8.26421 19.4525L8.73441 19.9075L9.20461 19.4525C9.899 18.7775 16.0131 12.735 16.0131 8.33333C16.011 6.12394 15.2434 4.00573 13.8789 2.44346C12.5143 0.881179 10.6642 0.00242633 8.73441 0V0ZM8.73441 12.5C8.01462 12.5 7.31099 12.2556 6.71251 11.7978C6.11402 11.34 5.64756 10.6892 5.37211 9.92785C5.09666 9.16649 5.02458 8.32871 5.16501 7.52046C5.30543 6.7122 5.65205 5.96977 6.16102 5.38706C6.66998 4.80434 7.31845 4.4075 8.02441 4.24673C8.73037 4.08596 9.46212 4.16847 10.1271 4.48384C10.7921 4.7992 11.3605 5.33325 11.7604 6.01846C12.1603 6.70366 12.3737 7.50924 12.3737 8.33333C12.3726 9.438 11.9888 10.497 11.3065 11.2782C10.6243 12.0593 9.69927 12.4987 8.73441 12.5Z" fill="#00295D" fill-opacity="0.5" />
                      <path d="M8.73438 10.8333C9.94035 10.8333 10.918 9.71396 10.918 8.33325C10.918 6.95254 9.94035 5.83325 8.73438 5.83325C7.52841 5.83325 6.55078 6.95254 6.55078 8.33325C6.55078 9.71396 7.52841 10.8333 8.73438 10.8333Z" fill="#00295D" fill-opacity="0.5" />
                    </g>
                    <defs>
                      <clipPath id="clip0_866_4032">
                        <rect width="17.4688" height="20" fill="white" />
                      </clipPath>
                    </defs>
                  </svg>
                  <span>Collection Address</span>
                </div>
              </th>
              <th class="search_input">
                <div class="new_input">
                  <svg width="20" height="20" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M14.5 25C20.299 25 25 20.299 25 14.5C25 8.70101 20.299 4 14.5 4C8.70101 4 4 8.70101 4 14.5C4 20.299 8.70101 25 14.5 25Z" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                    <path d="M21.9243 21.925L27.9994 28.0001" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                  </svg>
                  <input v-model="tableQuery" placeholder="Search Table" name="search" type="text" @focus="error = false">
                </div>
              </th>
            </tr>
            <tr v-for="(data, index) in filteredTable" :key="index" class="table-details">
              <td class="date">
                {{ detailedDate(data[0].collectionDate) }}
              </td>
              <td class="time">
                {{ data[0].collectionTime }}
              </td>
              <td class="address">
                <div class="address_ctn">
                  <svg width="18" height="20" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <g clip-path="url(#clip0_866_4032)">
                      <path d="M8.73441 0C6.80464 0.00242633 4.95451 0.881179 3.58996 2.44346C2.22541 4.00573 1.45787 6.12394 1.45575 8.33333C1.45575 12.735 7.56982 18.7775 8.26421 19.4525L8.73441 19.9075L9.20461 19.4525C9.899 18.7775 16.0131 12.735 16.0131 8.33333C16.011 6.12394 15.2434 4.00573 13.8789 2.44346C12.5143 0.881179 10.6642 0.00242633 8.73441 0V0ZM8.73441 12.5C8.01462 12.5 7.31099 12.2556 6.71251 11.7978C6.11402 11.34 5.64756 10.6892 5.37211 9.92785C5.09666 9.16649 5.02458 8.32871 5.16501 7.52046C5.30543 6.7122 5.65205 5.96977 6.16102 5.38706C6.66998 4.80434 7.31845 4.4075 8.02441 4.24673C8.73037 4.08596 9.46212 4.16847 10.1271 4.48384C10.7921 4.7992 11.3605 5.33325 11.7604 6.01846C12.1603 6.70366 12.3737 7.50924 12.3737 8.33333C12.3726 9.438 11.9888 10.497 11.3065 11.2782C10.6243 12.0593 9.69927 12.4987 8.73441 12.5Z" fill="#00295D" fill-opacity="0.5" />
                      <path d="M8.73438 10.8333C9.94035 10.8333 10.918 9.71396 10.918 8.33325C10.918 6.95254 9.94035 5.83325 8.73438 5.83325C7.52841 5.83325 6.55078 6.95254 6.55078 8.33325C6.55078 9.71396 7.52841 10.8333 8.73438 10.8333Z" fill="#00295D" fill-opacity="0.5" />
                    </g>
                    <defs>
                      <clipPath id="clip0_866_4032">
                        <rect width="17.4688" height="20" fill="white" />
                      </clipPath>
                    </defs>
                  </svg>
                  <span>{{ data[0].cAddress }}</span>
                </div>
              </td>
              <td class="action-ctn">
                <div class="action">
                  <svg
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                    @click="$router.push(`/${$route.name}/dismissed?id=${data[0].id}`)"
                  >
                    <rect width="24" height="24" rx="4" fill="#0FB2F3" />
                    <path d="M14.9778 10.6844L11.4078 7.11436C11.2621 6.96949 11.0649 6.88818 10.8595 6.88818C10.654 6.88818 10.4568 6.96949 10.3111 7.11436C10.2382 7.18666 10.1804 7.27268 10.1409 7.36746C10.1014 7.46224 10.0811 7.5639 10.0811 7.66658C10.0811 7.76925 10.1014 7.87091 10.1409 7.96569C10.1804 8.06047 10.2382 8.1465 10.3111 8.2188L13.8889 11.781C13.9618 11.8533 14.0197 11.9394 14.0591 12.0341C14.0986 12.1289 14.119 12.2306 14.119 12.3332C14.119 12.4359 14.0986 12.5376 14.0591 12.6324C14.0197 12.7271 13.9618 12.8132 13.8889 12.8855L10.3111 16.4477C10.1647 16.5931 10.082 16.7908 10.0812 16.9972C10.0805 17.2036 10.1618 17.4018 10.3072 17.5482C10.4527 17.6947 10.6503 17.7774 10.8567 17.7781C11.0631 17.7789 11.2613 17.6976 11.4078 17.5521L14.9778 13.9821C15.4147 13.5446 15.6602 12.9516 15.6602 12.3332C15.6602 11.7149 15.4147 11.1219 14.9778 10.6844Z" fill="white" />
                  </svg>
                </div>
              </td>
            </tr>
          </table>
          <TablesFooter
            :total-docs="totalData"
            :prev-disabled="hasPrevPage"
            :next-disabled="hasNextPage"
            :limit-props="limit"
            @set-limit="$emit('set-limit',$event)"
            @next="$emit('next')"
            @prev="$emit('prev')"
          />
          <div v-if="!filteredTable.length" class="come-down search_empty">
            <EmptyData
              :modal-head="'No Result!'"
              :modal-text="'You have no Order related to your search!'"
            />
          </div>
        </div>
        <div class="no_show">
          <div class="new_input">
            <svg width="20" height="20" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M14.5 25C20.299 25 25 20.299 25 14.5C25 8.70101 20.299 4 14.5 4C8.70101 4 4 8.70101 4 14.5C4 20.299 8.70101 25 14.5 25Z" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
              <path d="M21.9243 21.925L27.9994 28.0001" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
            </svg>
            <input v-model="tableQuery" placeholder="Search Table" name="search" type="text" @focus="error = false">
          </div>
          <TablesFooter
            :total-docs="totalData"
            :prev-disabled="hasPrevPage"
            :next-disabled="hasNextPage"
            :limit-props="limit"
            @set-limit="$emit('set-limit',$event)"
            @next="$emit('next')"
            @prev="$emit('prev')"
          />
          <div v-for="(data, index) in filteredTable" :key="index" class="data_box slide-in-from-left" @click="$router.push(`/${$route.name}/dismissed?id=${data[0].id}`)">
            <div>
              <p class="mobile_time">
                {{ data[0].collectionTime }}
              </p>
              <p class="mobile_date">
                {{ detailedDate(data[0].collectionDate) }}
              </p>
              <p class="mobile_address">
                <svg width="13" height="15" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <g clip-path="url(#clip0_866_4032)">
                    <path d="M8.73441 0C6.80464 0.00242633 4.95451 0.881179 3.58996 2.44346C2.22541 4.00573 1.45787 6.12394 1.45575 8.33333C1.45575 12.735 7.56982 18.7775 8.26421 19.4525L8.73441 19.9075L9.20461 19.4525C9.899 18.7775 16.0131 12.735 16.0131 8.33333C16.011 6.12394 15.2434 4.00573 13.8789 2.44346C12.5143 0.881179 10.6642 0.00242633 8.73441 0V0ZM8.73441 12.5C8.01462 12.5 7.31099 12.2556 6.71251 11.7978C6.11402 11.34 5.64756 10.6892 5.37211 9.92785C5.09666 9.16649 5.02458 8.32871 5.16501 7.52046C5.30543 6.7122 5.65205 5.96977 6.16102 5.38706C6.66998 4.80434 7.31845 4.4075 8.02441 4.24673C8.73037 4.08596 9.46212 4.16847 10.1271 4.48384C10.7921 4.7992 11.3605 5.33325 11.7604 6.01846C12.1603 6.70366 12.3737 7.50924 12.3737 8.33333C12.3726 9.438 11.9888 10.497 11.3065 11.2782C10.6243 12.0593 9.69927 12.4987 8.73441 12.5Z" fill="#00295D" />
                    <path d="M8.73438 10.8333C9.94035 10.8333 10.918 9.71396 10.918 8.33325C10.918 6.95254 9.94035 5.83325 8.73438 5.83325C7.52841 5.83325 6.55078 6.95254 6.55078 8.33325C6.55078 9.71396 7.52841 10.8333 8.73438 10.8333Z" fill="#00295D" />
                  </g>
                  <defs>
                    <clipPath id="clip0_866_4032">
                      <rect width="17.4688" height="20" fill="white" />
                    </clipPath>
                  </defs>
                </svg>
                <span>{{ data[0].cAddress }}</span>
              </p>
            </div>
            <div class="action_mobile">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect width="24" height="24" rx="4" fill="#0FB2F3" />
                <path d="M14.9778 10.6844L11.4078 7.11436C11.2621 6.96949 11.0649 6.88818 10.8595 6.88818C10.654 6.88818 10.4568 6.96949 10.3111 7.11436C10.2382 7.18666 10.1804 7.27268 10.1409 7.36746C10.1014 7.46224 10.0811 7.5639 10.0811 7.66658C10.0811 7.76925 10.1014 7.87091 10.1409 7.96569C10.1804 8.06047 10.2382 8.1465 10.3111 8.2188L13.8889 11.781C13.9618 11.8533 14.0197 11.9394 14.0591 12.0341C14.0986 12.1289 14.119 12.2306 14.119 12.3332C14.119 12.4359 14.0986 12.5376 14.0591 12.6324C14.0197 12.7271 13.9618 12.8132 13.8889 12.8855L10.3111 16.4477C10.1647 16.5931 10.082 16.7908 10.0812 16.9972C10.0805 17.2036 10.1618 17.4018 10.3072 17.5482C10.4527 17.6947 10.6503 17.7774 10.8567 17.7781C11.0631 17.7789 11.2613 17.6976 11.4078 17.5521L14.9778 13.9821C15.4147 13.5446 15.6602 12.9516 15.6602 12.3332C15.6602 11.7149 15.4147 11.1219 14.9778 10.6844Z" fill="white" />
              </svg>
            </div>
          </div>
          <div v-if="!filteredTable.length" class="come-down search_empty">
            <EmptyData
              :modal-head="'No Result!'"
              :modal-text="'You have no Order related to your search!'"
            />
          </div>
        </div>
      </div>
      <div v-else class="come-down">
        <EmptyData
          :modal-head="'No Dismissed Order!'"
          :modal-text="'You are all Caught up!'"
          :bg-btn="'See My Todo'"
          @bg-action="$router.push('/to-do-orders')"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { detailedDate } from '@/utils/date-formats.js'
import functions from '@/utils/functions'
// import Cookies from 'js-cookie'
export default {
  props: {
    tableData: {
      type: Array,
      default: () => []
    },
    hasPrevPage: {
      type: Boolean,
      default: () => null
    },
    hasNextPage: {
      type: Boolean,
      default: () => null
    },
    limit: {
      type: Number,
      default: () => 8
    },
    totalData: {
      type: Number,
      default: () => null
    },
    tableLoader: {
      type: Boolean,
      default: () => false
    }
  },
  data () {
    return {
      currency: functions.formatCurrency,
      detailedDate,
      tableQuery: '',
      transLoading: false
    }
  },
  computed: {
    filteredTable () {
      return this.tableData.filter(data => this.detailedDate(data[0].collectionDate).toLowerCase().includes(this.tableQuery.toLowerCase()) || data[0].collectionTime.toLowerCase().includes(this.tableQuery.toLowerCase()) || data[0].cAddress.toLowerCase().includes(this.tableQuery.toLowerCase()))
    }
  },
  methods: {
  }
}
</script>

<style scoped>

.table-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30px 30px;
}

.table-title {
  font-size: 22px;
  font-weight: 700;
  color: #3F3F3F;
}

.search-box {
  border: 1px solid #064a7b2c;
  height: 50px;
  background-color: #fafafa;
  display: flex;
  width: 25rem;
  padding: 0 15px;
  border-radius: 100px;
}

.view-all {
  font-size: 15px;
  cursor: pointer;
}
.table-loader {
  margin-top: 100px;
}
.table-container {
  background-color: #ffffff;
  border-radius: 10px;
  width: 100%;
  /* border: 1px solid #1A240; */
}

/* .table, tr {
  width: 100%;
} */

table, th, td,
td span {
  width: 100%;
  /* border: 1px solid #fff; */
  border-collapse: collapse;
  /* font-size: 15px; */
  font-weight: 600;
}
.table-header {
  height: 75px;
  background-color: #F2F4F7;
  padding: 0 20px;
  border-radius: 4px;
}

.table-header th,
th span {
  font-weight: 800;
  color: #000;
}
.table-details {
  height: 75px;
  padding: 0 20px;
}
.table-details:nth-child(odd) {
  height: 60px;
  background-color: #F9FAFB;
  border-radius: 4px;
  padding: 0 20px;
}
th {
  text-align: left;
}

 .date {
  width: 28%;
  padding-left: 25px;
}

.time {
  width: 17%;
}

.address {
  width: 30%;
}

.search_input {
  padding-right: 10px;
  width: 25%;
}

.address_ctn {
  display: flex;
  align-items: center;
  gap: 5px;
}

.action-ctn {
  padding-right: 10px;
  width: 25%;
}

.action {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.action_mobile {
  /* width: 5rem; */
  cursor: pointer;
}

.action svg {
  margin: 0 3px;
  cursor: pointer;
}

.type-details {
  width: 10rem;
  color: #EE3E3E;
}

.success {
  color: #4ABF21;
}

.amount {
  width: 13rem;
}

@media only screen and (max-width: 500px) {
  .data_box {
    border: 1px solid rgba(0, 41, 93, 0.06);
    box-shadow: 0px 4px 4px rgba(0, 41, 93, 0.04);
    border-radius: 10px;
    padding: 3vh 5vw;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 3vh;
    cursor: pointer;
  }
  .mobile_time {
    font-weight: 700;
    font-size: 16px;
    margin-bottom: 10px;
  }
  .mobile_date {
    font-weight: 600;
    font-size: 13px;
    margin-bottom: 10px;
  }
  .mobile_address {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .mobile_address span {
    font-size: 13px;
    color: rgba(0, 0, 0, 0.50);
  }

  .new_input {
    margin-bottom: 30px;
  }
}
</style>
