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
              <h6 class="msg-info">Please create an account</h6>

              <form @submit.prevent="register">
                <small
                  class="text-danger text-capitalize"
                  v-show="ErrorResponse"
                  ><strong>{{ ErrorResponse }}</strong></small
                >

                <div class="form-group">
                  <label class="form-control-label text-muted">Firstname</label>
                  <input
                    type="text"
                    name="firstname"
                    placeholder="First Name"
                    class="form-control"
                    v-model="details.firstname"
                  />
                  <small class="text-danger">{{ errors.firstname }}</small>
                </div>

                <div class="form-group">
                  <label class="form-control-label text-muted">Lastname</label>
                  <input
                    type="text"
                    name="lastname"
                    placeholder="Last Name"
                    class="form-control"
                    v-model="details.lastname"
                  />
                  <small class="text-danger">{{ errors.lastname }}</small>
                </div>
                <div class="form-group">
                  <label class="form-control-label text-muted">Email</label>
                  <input
                    type="email"
                    name="email"
                    placeholder="Email"
                    class="form-control"
                    v-model="details.email"
                  />
                  <small class="text-danger">{{ errors.email }}</small>
                </div>
                <div class="form-group">
                  <label class="form-control-label text-muted">Mobile</label>
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
                    id="psw"
                    name="psw"
                    placeholder="Password"
                    class="form-control"
                    v-model="details.password"
                  />
                  <small class="text-danger">{{ errors.password }}</small>
                </div>
                <div class="row justify-content-center my-3 px-3">
                  <button class="btn-block btn-color">Register</button>
                </div>
              </form>

              <div class="row justify-content-center my-2">
               <router-link to="/login">Already Have an Account?</router-link>
              </div>
            </div>
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
  name: "Register",
  data() {
    return {
      details: {
        firstname: "",
        lastname: "",
        email: "",
        mobile: "",
        password: "",
      },
      errors: {
        firstname: "",
        lastname: "",
        email: "",
        mobile: "",
        password: "",
      },
      ErrorResponse: "",
    };
  },
  methods: {
    async register() {
      //Validation
      if (!this.details.firstname)
        this.errors.firstname = "First Name Required";
      else this.errors.firstname = "";

      if (!this.details.lastname) this.errors.lastname = "Last Name Required";
      else this.errors.lastname = "";

      if (!this.details.email) this.errors.email = "Email Required";
      else this.errors.email = "";

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
        if (
          this.details.firstname &&
          this.details.lastname &&
          this.details.email &&
          this.details.password &&
          this.details.mobile
        ) {
          await axios.post(
            "https://test.firstbetng.com/api/v1/register",
            JSON.stringify(this.details),
            config
          );
          this.$router.push({
            name: "OTP",
            params: { mobile: this.details.mobile },
          });
        }
      } catch (err) {
        this.ErrorResponse = err.response.data.error.message;
      }
    },
  },
};
</script>

<style>
input,
textarea {
  background-color: #f3e5f5;
  border-radius: 50px !important;
  padding: 12px 15px 12px 15px !important;
  width: 100%;
  box-sizing: border-box;
  border: none !important;
  border: 1px solid #f3e5f5 !important;
  font-size: 16px !important;
  color: #000 !important;
  font-weight: 400;
}

input:focus,
textarea:focus {
  -moz-box-shadow: none !important;
  -webkit-box-shadow: none !important;
  box-shadow: none !important;
  border: 1px solid #d500f9 !important;
  outline-width: 0;
  font-weight: 400;
}

button:focus {
  -moz-box-shadow: none !important;
  -webkit-box-shadow: none !important;
  box-shadow: none !important;
  outline-width: 0;
}

.card {
  border-radius: 0;
  border: none;
}

.card1 {
  width: 50%;
  padding: 40px 30px 10px 30px;
}

.card2 {
  width: 50%;
  background-image: linear-gradient(to right, #ffd54f, #d500f9);
}

#logo {
  width: 70px;
  height: 60px;
}

.heading {
  margin-bottom: 60px !important;
}

::placeholder {
  color: #000 !important;
  opacity: 1;
}

:-ms-input-placeholder {
  color: #000 !important;
}

::-ms-input-placeholder {
  color: #000 !important;
}

.form-control-label {
  font-size: 12px;
  margin-left: 15px;
}

.msg-info {
  padding-left: 15px;
  margin-bottom: 30px;
}

.btn-color {
  border-radius: 50px;
  color: #fff;
  background-image: linear-gradient(to right, #ffd54f, #d500f9);
  padding: 15px;
  cursor: pointer;
  border: none !important;
  margin-top: 40px;
}

.btn-color:hover {
  color: #fff;
  background-image: linear-gradient(to right, #d500f9, #ffd54f);
}

.btn-white {
  border-radius: 50px;
  color: #d500f9;
  background-color: #fff;
  padding: 8px 40px;
  cursor: pointer;
  border: 2px solid #d500f9 !important;
}

.btn-white:hover {
  color: #fff;
  background-image: linear-gradient(to right, #ffd54f, #d500f9);
}

a {
  color: #000;
}

a:hover {
  color: #000;
}

.bottom {
  width: 100%;
  margin-top: 50px !important;
}

.sm-text {
  font-size: 15px;
}

@media screen and (max-width: 992px) {
  .card1 {
    width: 100%;
    padding: 40px 30px 10px 30px;
  }

  .card2 {
    width: 100%;
  }

  .right {
    margin-top: 100px !important;
    margin-bottom: 100px !important;
  }
}

@media screen and (max-width: 768px) {
  .container {
    padding: 10px !important;
  }

  .card2 {
    padding: 50px;
  }

  .right {
    margin-top: 50px !important;
    margin-bottom: 50px !important;
  }
}
</style>
