<template>
  <div class="topbar container-fluid text-white">
    <div class="h-25 px-5 py-2 row navbar justify-content-end">
      <div v-if="auth">
        <div class="dropdown">
          <button class="dropbtn">Xin Chào, {{ auth.user.full_name }}</button>
          <div class="dropdown-content text-left">
            <router-link to="/cart" class="dropdown-item">
              Giỏ Hàng
            </router-link>
            <a @click="logout" class="dropdown-item" href="#">Đăng Xuất</a>
          </div>
        </div>
      </div>
      <div v-else class="row mr-5">
        <router-link class="" to="/login">
          Đăng Nhập
        </router-link>
        <p style="margin:0px 10px">|</p>
        <router-link class="" to="/register">
          Đăng Ký
        </router-link>
      </div>
    </div>
  </div>
  <nav class="navbar navbar-expand-lg">
    <div class="collapse navbar-collapse mx-5" id="navbarSupportedContent">
      <a class="navbar-brand mr-auto" href="#">
        <img
          height="80"
          src="https://iweb.tatthanh.com.vn/pic/3/blog/images/logo-cua-hang-dong-ho%20(1).jpg"
          alt="logo"
        />
      </a>
      <form class="frmSearch" action="/search/" method="get">
        <div class="flex">
          <input
            type="text"
            name="keyword"
            placeholder="Nhập từ khóa tìm kiếm..."
          />
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 p-2"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
              clip-rule="evenodd"
            />
          </svg>
        </div>
      </form>
      <ul class="navbar-nav">
        <!-- Home -->
        <li class="nav-item mr-4">
          <router-link to="/" class="nav-link">Trang Chủ</router-link>
        </li>

        <!-- Brand -->
        <li class="nav-item dropdown mr-4">
          <a
            class="nav-link dropdown-toggle"
            href="#"
            id="brandDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            Thương Hiệu
          </a>
          <div class="dropdown-menu" aria-labelledby="brandDropdown">
            <div v-if="!brands.length" class="dropdown-item">
              <div class="d-flex justify-content-center">
                <div
                  class="spinner-grow spinner-grow-sm text-info"
                  role="status"
                >
                  <span class="sr-only">Loading...</span>
                </div>
              </div>
            </div>
            <div v-for="brand in brands" :key="brand.id">
              <router-link
                :to="{ path: '/brand/' + brand.name }"
                class="dropdown-item"
                :href="`brand/` + brand.name"
                >{{ brand.name }}</router-link
              >
            </div>
          </div>
        </li>

        <!--Category -->
        <li class="nav-item dropdown mr-4">
          <a
            class="nav-link dropdown-toggle"
            href="#"
            id="categoryDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            Danh Mục
          </a>
          <div class="dropdown-menu" aria-labelledby="categoryDropdown">
            <div v-if="!brands.length" class="dropdown-item">
              <div class="d-flex justify-content-center">
                <div
                  class="spinner-grow spinner-grow-sm text-info"
                  role="status"
                >
                  <span class="sr-only">Loading...</span>
                </div>
              </div>
            </div>
            <div v-for="category in categories" :key="category.id">
              <router-link
                :to="{ path: '/category/' + category.name }"
                class="dropdown-item"
                href="#"
                >{{ category.name }}</router-link
              >
            </div>
          </div>
        </li>

        <!--  -->
        <li class="nav-item">
          <router-link
            to="/about"
            class="nav-link"
            tabindex="-1"
            aria-disabled="true"
            >Về chúng tôi</router-link
          >
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { productService, userService } from "../../services/index";

export default {
  name: "NavBar",
  data() {
    return {
      categories: [],
      brands: [],
      auth: {
        access_token: String,
        expires_at: String,
        user: Object,
      },
    };
  },
  methods: {
    logout() {
      userService.logout();
      this.$router.push("/");
      window.location.href = "/";
    },
  },
  created() {
    productService
      .getCategory()
      .then((result) => {
        this.categories = result.data.data;
      })
      .catch((err) => {
        console.log(err);
      });
    productService
      .getBrand()
      .then((result) => {
        this.brands = result.data.data;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  mounted() {
    const auth = userService.auth();
    this.auth = auth;
  },
};
</script>

<style scoped>
.topbar a {
  color: white;
}
.navbar {
  background-color: #0e3a3b;
}
.navbar a {
  color: white;
}
.navbar a:hover {
  color: white;
}
.dropdown-menu a {
  color: black;
}
.dropdown-menu a:hover {
  color: black;
}

.frmSearch {
  display: flex;
  background: #fff;
  border-radius: 15px;
  width: 435px;
  height: 35px;
  overflow: hidden;
}

.frmSearch .flex {
  flex: 1;
  display: flex;
  position: relative;
}

.frmSearch .flex input {
  flex: 1;
  height: 35px;
  border: none;
  outline: none;
  padding: 0 15px;
  background: transparent;
}
.frmSearch .flex .btnSearch {
  height: 35px;
  width: 35px;
  line-height: 35px;
  text-align: center;
  background: transparent;
  border: none;
  cursor: pointer;
}

/* Dropdown Button */
.dropbtn {
  background-color: transparent;
  color: white;
  font-size: 16px;
  border: none;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Dropdown Content (Hidden by Default) */
.dropdown-content {
  display: none;
  position: absolute;
  z-index: 1;
  padding: 0.5rem 0;
  background-color: white;
  background-clip: padding-box;
  border: 1px solid #00000026;
  border-radius: 0.25rem;
}

/* Links inside the dropdown */
.dropdown-content a {
  color: black;
  text-decoration: none;
  display: block;
}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {
  display: block;
}
</style>
