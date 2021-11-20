<template>
  <div class="container mt-5">
    <div class="row d-flex justify-content-center">
      <div class="col-md-7">
        <div class="card p-3 py-4">
          <div class="text-center">
            <img
              src="https://i.imgur.com/bDLhJiP.jpg"
              width="100"
              class="rounded-circle"
            />
          </div>
          <div class="text-center mt-3">
            <span class="bg-secondary p-1 px-4 rounded text-white"
              >ID: {{ profile.customer_id }}</span
            >
            <h5 class="mt-2 mb-0">
              {{ profile.firstname }} {{ profile.lastname }}
            </h5>
            <span>{{ profile.mobile }}</span>
            <div class="px-4 mt-1">
              <p class="fonts">
                Consectetur adipiscing elit, sed do eiusmod tempor incididunt ut
                labore et dolore magna aliqua. Ut enim ad minim veniam, quis
                nostrud exercitation ullamco laboris nisi ut aliquip ex ea
                commodo consequat.
              </p>
            </div>
            <ul class="social-list">
              <li><i class="fa fa-facebook"></i></li>
              <li><i class="fa fa-dribbble"></i></li>
              <li><i class="fa fa-instagram"></i></li>
              <li><i class="fa fa-linkedin"></i></li>
              <li><i class="fa fa-google"></i></li>
            </ul>
            <div class="buttons">
              <button class="btn btn-outline-primary px-4">Message</button>
              <button class="btn btn-primary px-4 ms-3" @click="logout">
                Logout
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: "Dashboard",

  data() {
    return {
      token: "",
      profile: "",
    };
  },

  methods: {
    logout() {
      localStorage.removeItem("Token");
      this.$router.push({ name: "Login" });
    },
  },
  async created() {
    this.token = localStorage.Token;
    if (this.token) {
      const config = {
        headers: {
          Authorization: "Bearer " + this.token,
        },
      };
      try {
        const res = await axios.get(
          "https://test.firstbetng.com/api/v1/auth/profile",
          config
        );

        this.profile = res.data.success.data;
        console.log(this.profile);
      } catch (error) {
        this.$router.push({ name: "Login" });
      }
    } else {
      this.$router.push({ name: "Login" });
    }
  },
};
</script>


<style scoped>
.card {
  border: none;
  position: relative;
  overflow: hidden;
  border-radius: 8px;
  cursor: pointer;
}

.card:before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 4px;
  height: 100%;
  background-color: #e1bee7;
  transform: scaleY(1);
  transition: all 0.5s;
  transform-origin: bottom;
}

.card:after {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 4px;
  height: 100%;
  background-color: #8e24aa;
  transform: scaleY(0);
  transition: all 0.5s;
  transform-origin: bottom;
}

.card:hover::after {
  transform: scaleY(1);
}

.fonts {
  font-size: 11px;
}

.social-list {
  display: flex;
  list-style: none;
  justify-content: center;
  padding: 0;
}

.social-list li {
  padding: 10px;
  color: #8e24aa;
  font-size: 19px;
}

.buttons button:nth-child(1) {
  border: 1px solid #8e24aa !important;
  color: #8e24aa;
  height: 40px;
}

.buttons button:nth-child(1):hover {
  border: 1px solid #8e24aa !important;
  color: #fff;
  height: 40px;
  background-color: #8e24aa;
}

.buttons button:nth-child(2) {
  border: 1px solid #8e24aa !important;
  background-color: #8e24aa;
  color: #fff;
  height: 40px;
}
</style>