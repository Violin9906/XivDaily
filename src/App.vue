<template>
  <nav class="navbar navbar-expand-lg">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">XivDaily</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/subject">Subject</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>
        </ul>
        <div class="d-flex justify-content-between mb-2 mb-lg-0 col-lg-2">
          <span class="pe-lg-2 ps-lg-0 ps-5" role="button" @click="decDay()"
            >&lt;</span
          >
          <div>
            <span class="date-string" role="button" @click="pickDate()">
              {{ dateString }}
            </span>
            <input
              type="text"
              ref="dateInput"
              class="date-input"
              @hide="changeDate()"
            />
          </div>
          <span class="ps-lg-2 pe-lg-0 pe-5" role="button" @click="incDay()"
            >&gt;</span
          >
        </div>
      </div>
    </div>
  </nav>
  <router-view :date="today" />
</template>

<script>
import { Datepicker } from "vanillajs-datepicker";

export default {
  data() {
    return {
      today: new Date(),
      datePicker: null,
    };
  },
  watch: {
    today(newVal) {
      this.datePicker.setDate(newVal);
    },
  },
  methods: {
    incDay() {
      var newDate = new Date(this.today);
      newDate = newDate.setDate(newDate.getDate() + 1);
      this.today = new Date(newDate);
    },
    decDay() {
      var newDate = new Date(this.today);
      newDate = newDate.setDate(newDate.getDate() - 1);
      this.today = new Date(newDate);
    },
    pickDate() {
      // this.$refs.dateArea.focus();
      if (this.datePicker.active) {
        this.datePicker.hide();
      } else {
        this.datePicker.show();
      }
    },
    changeDate() {
      this.today = this.datePicker.getDate();
    },
  },
  computed: {
    dateString() {
      return this.today.toDateString();
    },
  },
  mounted() {
    this.datePicker = new Datepicker(this.$refs.dateInput, {
      autohide: true,
      todayBtn: true,
      todayBtnMode: 1,
    });
    this.datePicker.setDate(this.today);
  },
};
</script>

<style lang="less">
#app {
  font-family: "Times New Roman", Times, STSong, SimSun, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

nav {
  background: #1e50a2;
  color: #ffffff;

  .navbar-brand {
    color: #ffffff;
    &:hover,
    &:focus {
      color: #ffffff;
    }
  }

  .nav-link {
    font-weight: normal;
    color: #ffffff;
    &:hover,
    &:focus {
      color: #ffffff;
    }
    &:hover {
      -webkit-text-stroke-width: 0.6px;
      -webkit-text-stroke-color: #ffffff;
    }
  }

  .navbar-toggler-icon {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='rgba%28255, 255, 255, 0.55%29' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e");
  }

  .date-input {
    width: 0px;
    height: 0px;
    margin: 0px;
    padding: 0px;
    border: 0px;
    visibility: hidden;
  }
}
</style>
