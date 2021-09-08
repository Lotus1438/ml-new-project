<template>
  <div class="auth-wrapper auth-v2">
    <b-row class="auth-inner m-0">

      <!-- Brand logo-->
      <b-link class="brand-logo">
        <!-- <ml-logo /> -->
        <!-- <img
          :src="imgLogo"
          alt="ML Logo"> -->
        <!-- /////////////// -->
        <!-- <b-img
          fluid
          :src="imglogo"
          alt="MlLogo"
        /> -->
        <h2 class="brand-text text-danger ml-1">
          MLhuillier
        </h2>
      </b-link>
      <!-- /Brand logo-->

      <!-- Left Text-->
      <b-col
        lg="8"
        class="d-none d-lg-flex align-items-center p-5"
      >
        <div class="w-100 d-lg-flex align-items-center justify-content-center px-5">
          <b-img
            fluid
            :src="imgUrl"
            alt="Login V2"
          />
        </div>
      </b-col>
      <!-- /Left Text-->

      <!-- Login-->
      <b-col
        lg="4"
        class="d-flex align-items-center auth-bg px-2 p-lg-5"
      >
        <b-col
          sm="8"
          md="6"
          lg="12"
          class="px-xl-2 mx-auto"
        >
          <b-card-title
            title-tag="h2"
            class="font-weight-bold mb-1"
          >
            MLhuillier Evaluation Test!
          </b-card-title>
          <b-card-text class="mb-2">
            Please fill up input form
          </b-card-text>

          <!-- form -->
          <validation-observer ref="loginValidation">
            <b-form
              class="auth-register-form mt-2"
              @submit.prevent
            >

              <!-- name -->
              <b-form-group
                label="Full Name"
                label-for="name"
              >
                <validation-provider
                  #default="{ errors }"
                  name="Name"
                  rules="required"
                >
                  <b-form-input
                    id="name"
                    v-model="fullName"
                    :state="errors.length > 0 ? false:null"
                    name="name"
                  />
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- department -->
              <b-form-group
                id="department"
                label="Department"
                label-for="department"
              >
                <b-form-select
                  id="department"
                  v-model="form.department"
                  :options="department"
                  required
                />
              </b-form-group>

              <!-- email -->
              <b-form-group
                label="Email"
                label-for="login-email"
              >
                <validation-provider
                  #default="{ errors }"
                  name="Email"
                  rules="required|email"
                >
                  <b-form-input
                    id="login-email"
                    v-model="userEmail"
                    :state="errors.length > 0 ? false:null"
                    name="login-email"
                    placeholder="name@mlhuillier.com"
                  />
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- Password -->
              <b-form-group
                label="Password"
              >
                <validation-provider
                  #default="{ errors }"
                  name="Password"
                  rules="required"
                >
                  <b-input-group
                    class="input-group-merge"
                    :class="errors.length > 0 ? 'is-invalid':null"
                  >
                    <b-form-input
                      id="login-password"
                      v-model="password"
                      :state="errors.length > 0 ? false:null"
                      class="form-control-merge"
                      :type="passwordFieldType"
                      name="login-password"
                      placeholder="············"
                    />
                    <b-input-group-append is-text>
                      <feather-icon
                        class="cursor-pointer"
                        :icon="passwordToggleIcon"
                        @click="togglePasswordVisibility"
                      />
                    </b-input-group-append>
                  </b-input-group>
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- Confirm Password -->
              <b-form-group
                label="Confirm Password"
              >
                <validation-provider
                  #default="{ errors }"
                  name="Password"
                  rules="required"
                >
                  <b-input-group
                    class="input-group-merge"
                    :class="errors.length > 0 ? 'is-invalid':null"
                  >
                    <b-form-input
                      id="login-password"
                      v-model="password"
                      :state="errors.length > 0 ? false:null"
                      class="form-control-merge"
                      :type="passwordFieldType"
                      name="login-password"
                      placeholder="············"
                    />
                    <b-input-group-append is-text>
                      <feather-icon
                        class="cursor-pointer"
                        :icon="passwordToggleIcon"
                        @click="togglePasswordVisibility"
                      />
                    </b-input-group-append>
                  </b-input-group>
                  <small class="text-danger">{{ errors[0] }}</small>
                </validation-provider>
              </b-form-group>

              <!-- submit buttons -->
              <b-button
                type="submit"
                variant="danger"
                block
              >
                Register
              </b-button>
            </b-form>
          </validation-observer>

          <b-card-text class="text-center mt-2">
            <span>Already have an account? </span>
            <b-link :to="{name:'login'}">
              <span>&nbsp;Sign in</span>
            </b-link>
          </b-card-text>
        </b-col>
      </b-col>
    <!-- /Login-->
    </b-row>
  </div>
</template>

<script>
/* eslint-disable global-require */
import { ValidationProvider, ValidationObserver } from 'vee-validate'
// import VuexyLogo from '@core/layouts/components/Logo.vue'
import {
  BRow, BCol, BLink, BFormGroup, BFormInput, BInputGroupAppend, BInputGroup, BCardText, BCardTitle, BImg, BForm, BButton, BFormSelect,
} from 'bootstrap-vue'
import { required, email } from '@validations'
import { togglePasswordVisibility } from '@core/mixins/ui/forms'
import store from '@/store/index'
// import ToastificationContent from '@core/components/toastification/ToastificationContent.vue'

export default {
  components: {
    BRow,
    BCol,
    BLink,
    BFormGroup,
    BFormInput,
    BInputGroupAppend,
    BInputGroup,
    BCardText,
    BCardTitle,
    BImg,
    BForm,
    BButton,
    BFormSelect,
    // VuexyLogo,
    ValidationProvider,
    ValidationObserver,
  },
  mixins: [togglePasswordVisibility],
  data() {
    return {
      sideImg: require('@/assets/images/pages/register-share-goals.svg'),
      //   logo: require('@/assets/images/logo/logo.svg'),
      // validation rulesimport store from '@/store/index'
      form: {
        fullName: '',
        status: '',
        password: '',
        userEmail: '',
        required,
        email,
      },
      department: [{ text: 'TQA', value: null }, 'SNA', 'Dev.', 'Sys. Ad.'],
      show: true,
    }
  },
  computed: {
    passwordToggleIcon() {
      return this.passwordFieldType === 'password' ? 'EyeIcon' : 'EyeOffIcon'
    },
    // imglogo() {
    //   return this.imglogo
    // },
    imgUrl() {
      if (store.state.appConfig.layout.skin === 'dark') {
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.sideImg = require('@/assets/images/pages/register-share-goals.svg')
        return this.sideImg
      }
      return this.sideImg
    },
  },
  methods: {
    onSubmit(event) {
      event.preventDefault()
      alert(JSON.stringify(this.form))
    },
    // validationForm() {
    //   this.$refs.loginValidation.validate().then(success => {
    //     if (success) {
    //       this.$toast({
    //         component: ToastificationContent,
    //         props: {
    //           title: 'Form Submitted',
    //           icon: 'EditIcon',
    //           variant: 'success',
    //         },
    //       })
    //     }
    //   })
    // },
  },
}
</script>

<style lang="scss">
@import '@core/scss/vue/pages/page-auth.scss';
</style>
