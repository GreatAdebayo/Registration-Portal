<template>
  <div class="container px-4 py-5 mx-auto">
    <div class="card card0">
      <div class="d-flex flex-lg-row flex-column-reverse">
        <div class="card card1">
          <div class="row justify-content-center my-auto">
            <div class="col-md-8 col-10 my-5">
              <div class="row justify-content-center px-3 mb-3">
                <img id="logo" src="https://i.imgur.com/PSXxjNY.png" />
              </div>
              <h3 class="mb-5 text-center heading">We are Tidi</h3>
              <h6 class="msg-info">Please login to your account</h6>
              <form @submit.prevent="login">
                <small
                  class="text-danger text-capitalize"
                  v-show="ErrorResponse"
                  ><strong>{{ ErrorResponse }}</strong></small
                >
                <div class="form-group">
                  <label class="form-control-label text-muted"
                    >Mobile Number</label
                  >
                  <input
                    type="phone"
                    name="mobile"
                    placeholder="Mobile Number"
                    class="form-control"
                    v-model="details.mobile"
                  />
                  <small class="text-danger">{{ errors.mobile }}</small>
                </div>
                <div class="form-group">
                  <label class="form-control-label text-muted">Password</label>
                  <input
                    type="password"
                    name="passsword"
                    placeholder="Password"
                    class="form-control"
                    v-model="details.password"
                  />
                  <small class="text-danger">{{ errors.password }}</small>
                </div>
                <div class="row justify-content-center my-3 px-3">
                  <button class="btn-block btn-color">Login to Tidi</button>
                </div>
              </form>
              <div class="row justify-content-center my-2">
                <a href="#"
                  ><small class="text-muted">Forgot Password?</small></a
                >
              </div>
            </div>
          </div>
          <div class="bottom text-center mb-5">
            <p href="#" class="sm-text mx-auto mb-3">
              Don't have an account?<router-link  to='/' class="btn btn-white ml-2">
                Create new
              </router-link>
            </p>
          </div>
        </div>
        <div class="card card2">
          <div class="my-auto mx-md-5 px-md-5 right">
            <h3 class="text-white">We are more than just a company</h3>
            <small class="text-white"
              >Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
              eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
              enim ad minim veniam, quis nostrud exercitation ullamco laboris
              nisi ut aliquip ex ea commodo consequat.</small
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Login",

  data() {
    return {
      details: {
        mobile: "",
        password: "",
      },
      errors: {
        mobile: "",
        password: "",
      },
      ErrorResponse: "",
    };
  },

  methods: {
    async login() {
      //Validation
      if (!this.details.mobile) this.errors.mobile = "Mobile Number Required";
      else this.errors.mobile = "";

      if (!this.details.password) this.errors.password = "Password Required";
      else this.errors.password = "";

      const config = {
        headers: {
          "Content-Type": "application/json",
        },
      };
      try {
        if (this.details.password && this.details.mobile) {
          const res = await axios.post(
            "https://test.firstbetng.com/api/v1/login",
            JSON.stringify(this.details),
            config
          );
          localStorage.setItem("Token", res.data.success.token);
          this.$router.push({ name: "Dashboard" });
        }
      } catch (err) {
        this.ErrorResponse = err.response.data.error.message;
      }
    },
  },
};
</script>