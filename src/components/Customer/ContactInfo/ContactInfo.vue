<template>
  <div class="main-holdd">
    <q-dialog v-model="phonedialog">
      <q-card style="width: 673px; max-width: 80vw">
        <div class="dialogmain">
          <q-toolbar class="toolbar-holder">
            <p class="phone-txt">Phone</p>
            <q-btn flat round dense icon="close" v-close-popup />
          </q-toolbar>
          <div class="radio-holder">
            <p class="category-txt">Category <span class="req">*</span></p>
            <div class="radio-class">
              <q-radio
                dense
                v-model="type"
                val="Personal"
                label="Peronal"
                class="radio-1"
              />
              <q-radio
                dense
                v-model="type"
                val="Company"
                label="Company"
                class="radio-1"
              />
              <q-radio
                dense
                v-model="type"
                val="Fax"
                label="Fax"
                class="radio-2"
              />
              <q-radio
                dense
                v-model="type"
                val="Other"
                label="Other"
                class="radio-2"
              />
            </div>
            <p class="channel-txt">Channel <span class="req">*</span></p>
            <div class="checkbox-class">
              <div class="q-pa-md">
                <div class="q-gutter-sm">
                  <div>
                    <q-checkbox
                      left-label
                      val="whatsapp"
                      v-model="selection"
                      label="WhatsApp"
                      class="checkbox-whatsapp"
                      :rules="[selectRules]"
                    />
                    <q-checkbox
                      left-label
                      val="line"
                      v-model="selection"
                      label="LINE"
                      class="checkbox-line"
                      :rules="[selectRules]"
                    />
                    <q-checkbox
                      left-label
                      val="wechat"
                      v-model="selection"
                      label="Wechat"
                      class="checkbox-wechat"
                      :rules="[selectRules]"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div class="field-holderr">
              <p class="category-txt">
                Phone Number <span class="req">*</span>
              </p>
              <div class="col">
                <q-select
                  outlined
                  v-model="phoneNumber"
                  :options="optionsPhoneNumber"
                  :rules="selectRules"
                  dense
                  class="input-individual"
                />
              </div>
            </div>
            <div class="field-holderr">
              <p class="category-txt">Remarks</p>
              <div class="col">
                <q-input
                  outlined
                  v-model="remarks"
                  dense
                  class="input-individual"
                />
              </div>
            </div>
            <div class="lowerdialog-btn">
              <q-btn
                color="primary"
                label="Save"
                v-close-popup
                @click="addPhone"
              />
            </div>
          </div>
        </div>
      </q-card>
    </q-dialog>

    <q-dialog v-model="addressdialog">
      <q-card style="width: 673px; max-width: 80vw">
        <div class="dialogmain">
          <q-toolbar class="toolbar-holder">
            <p class="address-txt">Address</p>
            <q-btn flat round dense icon="close" v-close-popup />
          </q-toolbar>
          <div class="radio-holder">
            <p class="type-txt">Type</p>
            <div class="radio-class">
              <q-radio
                dense
                v-model="type"
                val="home"
                label="Home"
                class="radio-1"
              />
              <q-radio
                dense
                v-model="type"
                val="company"
                label="Company"
                class="radio-2"
              />
              <q-radio
                dense
                v-model="type"
                val="fax"
                label="Delivery Address"
                class="radio-2"
              />
            </div>
            <div class="field-holderr">
              <div class="rowdialog">
                <div class="padding-1">
                  <div class="field-holderr">
                    <p class="type-txt">Country <span class="req">*</span></p>
                    <q-select
                      outlined
                      dense
                      v-model="selectModel"
                      :options="optionsCountry"
                      :rules="selectRules"
                    />
                  </div>
                </div>
                <div class="padding-2">
                  <div class="field-holderr">
                    <p class="type-txt">
                      Country Code <span class="req">*</span>
                    </p>
                    <q-input
                      outlined
                      v-model="inputCountryCode"
                      dense
                      :rules="inputRules"
                    />
                  </div>
                </div>
              </div>
              <div class="rowdialog">
                <div class="padding-1">
                  <div class="field-holderr">
                    <p class="type-txt">ZIP</p>
                    <q-input outlined v-model="inputZIP" dense />
                  </div>
                </div>
                <div class="padding-2">
                  <div class="field-holderr">
                    <p class="type-txt">City <span class="req">*</span></p>
                    <q-input
                      outlined
                      v-model="inputCity"
                      dense
                      :rules="inputRules"
                    />
                  </div>
                </div>
              </div>
              <div class="rowdialog">
                <div class="padding-1">
                  <div class="field-holderr">
                    <p class="type-txt">State/Province</p>
                    <q-input outlined v-model="inputStateProvince" dense />
                  </div>
                </div>
                <div class="padding-2">
                  <div class="field-holderr">
                    <p class="type-txt">Street <span class="req">*</span></p>
                    <q-input
                      outlined
                      v-model="inputStreet"
                      dense
                      :rules="inputRules"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div class="field-holderr">
              <p class="type-txt">Remark</p>
              <div class="col">
                <q-input outlined v-model="inputRemark" dense />
              </div>
            </div>
            <div class="checkbox-class">
              <div class="q-pa-md">
                <div class="q-gutter-sm">
                  <div>
                    <q-checkbox
                      val="isActive"
                      v-model="selection"
                      label="Is Active"
                      class="checkbox-isActive"
                    />
                  </div>
                </div>
              </div>
            </div>

            <div class="lowerdialog-btn">
              <q-btn color="primary" label="Save" v-close-popup />
            </div>
          </div>
        </div>
      </q-card>
    </q-dialog>

    <div class="sub-hold">
      <div class="row contactInformation-content">
        <div class="col-3">
          <div class="row-main">
            <div>
              <div
                :class="
                  selectedtab === 'Phone' ? 'sidebar-row-active' : 'sidebar-row'
                "
                @click="handleclick('Phone')"
              >
                <img
                  src="../../../assets/images/phonewhite.png"
                  v-if="selectedtab === 'Phone'"
                />
                <img
                  src="../../../assets/images/phone.png"
                  v-if="selectedtab !== 'Phone'"
                />

                <p
                  :class="
                    selectedtab === 'Phone'
                      ? 'sidebar-subtext-active'
                      : 'sidebar-subtext'
                  "
                >
                  Phone
                </p>
              </div>
            </div>

            <div>
              <div
                :class="
                  selectedtab === 'Address'
                    ? 'sidebar-row-active'
                    : 'sidebar-row'
                "
                @click="handleclick('Address')"
              >
                <img
                  src="../../../assets/images/addresswhite.png"
                  v-if="selectedtab === 'Address'"
                />
                <img
                  src="../../../assets/images/address.png"
                  v-if="selectedtab !== 'Address'"
                />
                <p
                  :class="
                    selectedtab === 'Address'
                      ? 'sidebar-subtext-active'
                      : 'sidebar-subtext'
                  "
                >
                  Address
                </p>
              </div>
            </div>
          </div>
        </div>
        <div class="contactInformation-content_center">
          <div>
            <div class="row justify-between">
              <q-btn
                v-if="
                  customerStore.customer.contacts && selectedtab === 'Phone'
                "
                style="background: #4b44f6; color: white"
                label="+ Add"
                @click="phonedialog = true"
              />
            </div>
            <div
              v-if="customerStore.customer.contacts && selectedtab === 'Phone'"
              class="row q-col-gutter-md"
            >
              <div
                v-for="(contact, index) in customerStore.customer.contacts"
                :key="index"
              >
                <contact-phone-card
                  :phone-number="contact.contacts_id.phone_number"
                  :remarks="`This is ${contact.contacts_id.remarks} number`"
                  @edit="phonedialog = true"
                />
              </div>
            </div>
            <div v-else class="row justify-center">
              <div style="align-items: center">
                <div>
                  <img
                    class="inline-block"
                    src="../../../assets/images/otherinfomain.png"
                  />

                  <p class="bottom-textmainn">No {{ selectedtab }}</p>
                </div>
                <p v-if="selectedtab === 'Phone'" class="bottom-textsubb">
                  {{ phonetxt }}
                </p>
                <p v-if="selectedtab === 'Address'" class="bottom-textsubb">
                  {{ addresstxt }}
                </p>

                <q-btn
                  v-if="selectedtab === 'Phone'"
                  color="primary"
                  icon="add"
                  label="New phone"
                  no-caps
                  @click="phonedialog = true"
                  class="modal-btn"
                />
                <q-btn
                  v-if="selectedtab === 'Address'"
                  color="primary"
                  icon="add"
                  label="New address"
                  no-caps
                  @click="addressdialog = true"
                  class="modal-btn"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import "./ContactInfo.scss";
// import "vue3-tel-input/dist/vue3-tel-input.css";
import ContactPhoneCard from "../ContactPhoneCard.vue";
import { useRoute } from "vue-router";
import useCustomerStore from "src/stores/modules/customer";

const route = useRoute();
const customerStore = useCustomerStore();

const phonedialog = ref(false);
const addressdialog = ref(false);
const phoneNumber = ref("");
const remarks = ref("");

const inputCountryCode = ref("");
const inputZIP = ref("");
const inputCity = ref("");
const inputStateProvince = ref("");
const inputStreet = ref("");
const inputRemark = ref("");

const type = ref("");
const selectModel = ref(null);
const optionsPhoneNumber = ["", "Example"];
const optionsCountry = ["", "Example"];
const selection = ref([""]);

const selectRules = [
  (val) => (val && val.length > 0) || "Please choose something",
];
const inputRules = [
  (val) => (val && val.length > 0) || "Please type something",
];
const selectedtab = ref("Phone");
const phonetxt = ref("Click the button to add the first call");
const addresstxt = ref("Click the button below to add address information.");

const handleclick = (data) => {
  selectedtab.value = data;
};

const addPhone = async () => {
  const customerId = route.params.id;
  const params = {
    category: type.value,
    channel: selection.value,
    phone_number: phoneNumber.value,
    remarks: remarks.value,
  };
  const result = await customerStore.addContact(customerId, params);
  console.log(result);
};
</script>

<style lang="sass" scoped>

.row>div.col-3
  padding: 10px 15px
  background: white
  border-right: 1px solid rgba(86,61,124,.2)
.row + .row
  margin-top: 1rem
</style>
