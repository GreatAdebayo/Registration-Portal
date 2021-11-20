<template>
  <div class="container px-4 py-5 mx-auto">
    <div class="card card2">
      <div class="my-auto mx-md-5 px-md-5 right">
        <h1>Verify Your Account</h1>
        <form @submit.prevent="verify">
          <small class="text-danger"><strong>{{ errRes }}</strong></small>
          <div class="form-group">
            <label class="form-control-label text-muted">OTP</label>
            <input
              type="number"
              name="OTP"
              placeholder="OTP"
              class="form-control"
              v-model="otp"
            />
          </div>

          <div class="row justify-content-center my-3 px-3">
            <button class="btn-block btn-color">Verify</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "OTP",
  data() {
    return {
      mobile: this.$route.params.mobile,
      otp: "",
      errRes: "",
    };
  },

  methods: {
    async verify() {
      if (this.otp) {
        const config = {
          headers: {
            "Content-Type": "application/json",
          },
        };
        try {
          await axios.post(
            "https://test.firstbetng.com/api/v1/validate-otp",
            JSON.stringify({ otp: this.otp, mobile: this.mobile }),
            config
          );
          this.$router.push({ name: "Login"});
        } catch (err) {
          this.errRes = err.response.data.error.message;
        }
      }
    },
  },
};
</script>