<template>
  <header class="header header-absolute">
    <!-- Navbar-->
    <nav
      class="navbar navbar-expand-lg navbar-sticky navbar-airy navbar-dark bg-fixed-white navbar-fixed-light"
      style="background: #000502"
    >
      <div class="container-fluid">
        <!-- Navbar Header  -->
        <router-link
          class="navbar-brand"
          style="height: fit-content !important"
          to="/"
        >
          <img src="@/assets/longWhite.png" class="logoImg" alt="" />
          <!-- <img src="@/assets/new-deco.png" class="logoImg" style="width:41px!important;" alt=""> -->
        </router-link>
        <button
          class="navbar-toggler"
          style="margin-bottom: 4px"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarCollapse"
          aria-controls="navbarCollapse"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <img
            src="@/assets/menu.png"
            style="width: 20px; margin: auto"
            alt=""
          />
        </button>
        <!-- Navbar Collapse -->
        <div class="collapse navbar-collapse" id="navbarCollapse">
          <ul class="mx-auto navbar-nav">
            <li v-on:click="toHome()" class="nav-item">
              <router-link
                to="/"
                data-bs-toggle="collapse"
                data-bs-target="#navbarCollapse"
                aria-controls="navbarCollapse"
                style="font-size: 12.4px; letter-spacing: 1px; font-weight: 600"
                class="nav-link"
                >Inicio</router-link
              >
            </li>
            <li v-on:click="toProducts()" class="nav-item">
              <router-link
                to="/products"
                data-bs-toggle="collapse"
                data-bs-target="#navbarCollapse"
                aria-controls="navbarCollapse"
                style="font-size: 12.4px; letter-spacing: 1px; font-weight: 600"
                class="nav-link"
                >Productos</router-link
              >
            </li>

            <!-- Megamenu-->
            <li class="nav-item dropdown position-static">
              <a
                style="font-size: 12.4px; letter-spacing: 1px; font-weight: 600"
                class="nav-link dropdown-toggle"
                href="#"
                data-bs-toggle="dropdown"
                >Categorias</a
              >
              <div
                class="dropdown-menu dropdown-menu-animated megamenu"
                style="left: auto !important"
              >
                <div class="row">
                  <div class="col-lg-12">
                    <div class="p-3 row">
                      <div v-for="item in categories" class="col-auto">
                        <!-- Megamenu list-->
                        <h6 class="text-uppercase" style="margin-bottom: 12px">
                          {{ item.category.name }}
                        </h6>
                        <ul class="megamenu-list list-unstyled">
                          <li
                            v-on:click="redirectToSubcategory(subitem)"
                            class="megamenu-list-item"
                            v-for="subitem in item.subcategories"
                          >
                            <a
                              class="megamenu-list-link"
                              data-bs-toggle="collapse"
                              data-bs-target="#navbarCollapse"
                              aria-controls="navbarCollapse"
                              style="cursor: pointer"
                            >
                              {{ subitem.name }}
                            </a>
                          </li>
                        </ul>
                        <!-- Megamenu list-->
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </li>
          </ul>

          <!-- Search Button Desktop-->
          <div
            class="mt-1 mb-2 d-flex align-items-center justify-content-center justify-content-lg-end my-lg-0 desktop"
            style="margin-right: 10px"
          >
            <div
              class=""
              style="
                display: flex;
                align-items: center;
                background-color: white;
                border-radius: 25px;
                height: 30px;
              "
              data-bs-toggle="search"
            >
              <div
                class=""
                style="
                  height: 30px;
                  width: 28px;
                  display: flex;
                  align-items: center;
                  justify-content: center;
                  padding-left: 12px;
                "
              >
                <img
                  src="@/assets/search-interface-symbol.png"
                  style="width: 13px"
                  alt=""
                />
              </div>
              <input
                v-on:keyup.enter="search()"
                v-model="filter"
                class="form-control"
                type="search"
                placeholder="Buscar"
                aria-label="Search"
                style="
                  border-radius: 25px;
                  border: none;
                  height: 30px;
                  font-size: 13px;
                "
              />
            </div>
          </div>

          <div
            class="mt-1 mb-2 d-flex align-items-center justify-content-between justify-content-lg-end my-lg-0"
          >
            <!-- User Not Logged - link to login page-->
            <div class="nav-item">
              <router-link
                v-if="!loggedIn"
                class="navbar-icon-link desktop"
                to="/login"
              >
                <img src="/assets/icons/user.png" style="width: 25px" />
                <span
                  class="text-sm ms-2 ms-lg-0 text-uppercase fw-bold d-none d-sm-inline d-lg-none"
                  >&nbsp; Iniciar Sesión</span
                >
              </router-link>
              <router-link
                v-if="!loggedIn"
                class="navbar-icon-link mobile"
                to="/login"
              >
                <img
                  data-bs-toggle="collapse"
                  data-bs-target="#navbarCollapse"
                  aria-controls="navbarCollapse"
                  src="/assets/icons/user.png"
                  style="width: 25px"
                />
                <span
                  data-bs-toggle="collapse"
                  data-bs-target="#navbarCollapse"
                  aria-controls="navbarCollapse"
                  class="text-sm ms-2 ms-lg-0 text-uppercase fw-bold d-none d-sm-inline d-lg-none"
                  >&nbsp; Iniciar Sesión</span
                >
              </router-link>

              <router-link
                to="/profile/address"
                v-if="loggedIn"
                class="navbar-icon-link mobile"
              >
                <img
                  src="/assets/icons/user.png"
                  style="width: 25px"
                  data-bs-toggle="collapse"
                  data-bs-target="#navbarCollapse"
                  aria-controls="navbarCollapse"
                />
                <span
                  data-bs-toggle="collapse"
                  data-bs-target="#navbarCollapse"
                  aria-controls="navbarCollapse"
                  class="text-sm ms-2 ms-lg-0 text-uppercase fw-bold d-none d-sm-inline d-lg-none"
                  >&nbsp; Mis domicilios</span
                >
              </router-link>

              <a v-if="loggedIn" class="navbar-icon-link dropdown desktop">
                <img src="/assets/icons/user.png" style="width: 25px" />
                <span
                  class="text-sm ms-2 ms-lg-0 text-uppercase fw-bold d-none d-sm-inline dropdown-toggle"
                  data-bs-target="#"
                  style="
                    letter-spacing: 0.5px !important;
                    font-size: 13px !important;
                  "
                  data-bs-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                  >&nbsp; {{ username.split(" ")[0] }}</span
                >
                <div
                  class="dropdown-menu dropdown-menu-animated"
                  aria-labelledby="categoryDropdownMenuLink"
                  style="left: -20px !important; bottom: 45px !important"
                >
                  <router-link
                    class="dropdown-item"
                    style="background-color: white"
                    to="/profile/address"
                    >Mis domicilios</router-link
                  >
                  <router-link
                    class="dropdown-item"
                    style="background-color: white"
                    to="/profile/orders"
                    >Mis pedidos</router-link
                  >
                  <a
                    class="dropdown-item"
                    style="background-color: white"
                    v-on:click="logOut()"
                    >Cerrar Sesión</a
                  >
                </div>
              </a>
            </div>
            <!-- search mobile -->
            <div
              class="mobile"
              style="
                display: flex;
                align-items: center;
                background-color: white;
                border-radius: 25px;
                height: 32px;
              "
              data-bs-toggle="search"
            >
              <div
                class=""
                style="
                  height: 32px;
                  width: 28px;
                  display: flex;
                  align-items: center;
                  justify-content: center;
                  padding-left: 15px;
                "
              >
                <img
                  src="@/assets/search-interface-symbol.png"
                  style="width: 16px"
                  alt=""
                />
              </div>
              <input
                v-on:keyup.enter="search()"
                v-model="filter"
                class="form-control"
                type="search"
                placeholder="Buscar"
                aria-label="Search"
                style="border-radius: 25px; border: none; height: 32px"
              />
            </div>
            <!-- Cart Dropdown-->
            <div class="nav-item dropdown">
              <router-link to="/cart" class="navbar-icon-link d-lg-none">
                <img
                  data-bs-toggle="collapse"
                  data-bs-target="#navbarCollapse"
                  aria-controls="navbarCollapse"
                  src="/assets/icons/cart.png"
                  style="width: 25px"
                />
                <span
                  data-bs-toggle="collapse"
                  data-bs-target="#navbarCollapse"
                  aria-controls="navbarCollapse"
                  class="text-sm ms-2 ms-lg-0 text-uppercase fw-bold d-none d-sm-inline d-lg-none"
                  >Carrito</span
                >
              </router-link>
              <div class="d-none d-lg-block">
                <a
                  class="navbar-icon-link"
                  id="cartdetails"
                  href="cart.html"
                  data-bs-target="#"
                  data-bs-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  <img src="/assets/icons/cart.png" style="width: 25px" />
                  <div class="navbar-icon-link-badge">{{ cart.length }}</div>
                </a>

                <div
                  class="p-4 dropdown-menu dropdown-menu-animated dropdown-menu-end"
                  style="
                    height: fit-content;
                    border: 1px solid rgba(0, 0, 0, 0.1);
                    border-radius: 0 0 6px 6px;
                  "
                  aria-labelledby="cartdetails"
                >
                  <div
                    v-if="cart.length > 0"
                    style="width: fit-content; height: fit-content"
                  >
                    <div
                      class="navbar-cart-product-wrapper"
                      style="max-height: 370px !important"
                    >
                      <!-- cart item-->
                      <div class="navbar-cart-product" v-for="item in cart">
                        <div class="d-flex align-items-center">
                          <a href="detail.html">
                            <img
                              class="img-fluid navbar-cart-product-image"
                              :src="item.product.image"
                              alt="..."
                          /></a>
                          <div class="w-100">
                            <a
                              class="navbar-cart-product-close"
                              v-on:click="deleteItem(item._id)"
                            >
                              <img
                                src="/assets/icons/close.png"
                                style="width: 13px; height: 13px"
                              />
                            </a>
                            <div class="ps-3">
                              <router-link
                                :to="/product/ + item.product.slug"
                                class="navbar-cart-product-link"
                                style="
                                  text-overflow: ellipsis;
                                  overflow: hidden;
                                  white-space: nowrap;
                                "
                              >
                                {{ item.product.name }}
                              </router-link>
                              <small class="d-block text-muted"
                                >Cantidad: {{ item.amountOfProducts }}</small
                              >
                              <!-- <small class="d-block text-muted">{{ item.product.str_variant }}: {{ item.variant.variant }} </small> -->
                              <strong
                                class="text-sm d-block"
                                v-if="USDEnabled == false"
                                >{{
                                  priceConverter(
                                    item.product.price *
                                      item.amountOfProducts *
                                      USDData.value
                                  )
                                }}
                              </strong>
                              <strong
                                class="text-sm d-block"
                                v-if="USDEnabled == true"
                                >{{
                                  priceConverter(
                                    item.product.price * item.amountOfProducts
                                  )
                                }}
                              </strong>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                    <!-- total price-->
                    <div class="navbar-cart-total">
                      <span class="text-muted">TOTAL</span>
                      <span v-if="USDEnabled == false" style="font-weight: 800"
                        >{{ priceConverter(total * USDData.value) }}
                      </span>
                      <span v-if="USDEnabled == true" style="font-weight: 800"
                        >{{ priceConverter(total) }}
                      </span>
                    </div>
                    <!-- buttons-->
                    <div class="d-flex justify-content-between">
                      <div
                        style="display:flex; flex-direction: column; align-items:center; justify-content:center; height"
                      >
                        <router-link class="viewCartBtn" to="/cart"
                          >Ver carrito</router-link
                        >
                      </div>

                      <router-link to="/checkout" class="cartBuyBtn"
                        >Comprar</router-link
                      >
                    </div>
                  </div>

                  <div
                    style="
                      min-width: 230px;
                      height: 70px;
                      display: flex;
                      flex-direction: column;
                      align-items: center;
                      justify-content: space-between;
                    "
                    v-if="cart.length === 0"
                  >
                    <span style="font-size: 19px; font-weight: 700"
                      >Tu carrito está vacío.</span
                    >
                    <router-link to="/products" class="cartBuyBtn"
                      >Agregar Productos</router-link
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <!-- /Navbar -->

    <!-- bottom Bar-->
    <div class="top-bar" style="height: 35px !important">
      <div class="container-fluid" style="height: 38px !important">
        <div
          class="justify-content-center row d-flex align-items-center"
          style="height: 35px !important; background-color: #1c4c3b"
        >
          <span
            class="text-white text-uppercase"
            style="
              font-size: 0.7rem;
              font-weight: 600;
              width: fit-content;
              letter-spacing: 0px;
            "
          >
            <span style="text-decoration: none" class="emoji">
              {{ headerMessage }}
            </span>
          </span>
        </div>
      </div>
    </div>
    <!-- bottom Bar End-->
  </header>
</template>

<style>
.emoji {
  font-family: "Segoe UI Emoji", "Apple Color Emoji", sans-serif;
}
.viewCartBtn {
  text-transform: uppercase;
  letter-spacing: 0.07em;
  line-height: 1.5;
  padding: 0.7rem 0.75rem;
  font-size: 0.6875rem;
  color: black;
  transition: all 0.3s ease-in-out;
  font-weight: 600;
}

.viewCartBtn:hover {
  color: #1c4c3b;
  text-decoration: none;
  transition: all 0.3s ease-in-out;
}

.cartBuyBtn {
  text-transform: uppercase;
  letter-spacing: 0.07em;
  line-height: 1.3;
  padding: 0.6rem 0.75rem;
  font-size: 0.6875rem;
  border-radius: 5px;
  width: fit-content;
  height: fit-content;
  background-color: #1c4c3b;
  color: white;
  text-decoration: none;
  transition: all 0.3s ease-in-out;
  font-weight: 600;
}

.cartBuyBtn:hover {
  color: white;
  text-decoration: none;
  transition: all 0.3s ease-in-out;
}

.mobile {
  display: none !important;
}

.desktop {
  display: flex !important;
}

.navbar.fixed-top.bg-fixed-white {
  background-color: #000000 !important ;
}

.navbar {
  padding-top: 0rem !important;
  padding-bottom: 0rem !important;
}

.navbar-icon-link-badge {
  position: absolute;
  top: -5px;
  right: -8px;
  width: 20px;
  height: 20px;
  text-align: center;
  color: #fff;
  border-radius: 50%;
  background: #343a40;
  font-size: 0.7rem;
  font-weight: 800;
  line-height: 20px;
}

.navbar-light .navbar-icon-link,
.navbar-fixed-light.fixed-top .navbar-icon-link,
.navbar-hover-light:hover .navbar-icon-link {
  color: rgba(255, 255, 255, 1);
}

.navbar-dark .navbar-icon-link-badge,
.navbar-fixed-light.fixed-top .navbar-icon-link-badge,
.navbar-hover-light:hover .navbar-icon-link-badge {
  color: white;
  background: #1c4c3b;
}

.navbar-light .navbar-nav .nav-link,
.navbar-hover-light:hover .navbar-nav .nav-link,
.navbar-fixed-light.fixed-top .navbar-nav .nav-link {
  color: rgba(255, 255, 255, 1);
  font-weight: 300;
}

.navbar-light .navbar-nav .show > .nav-link,
.navbar-light .navbar-nav .active > .nav-link,
.navbar-light .navbar-nav .nav-link.show,
.navbar-light .navbar-nav .nav-link.active,
.navbar-hover-light:hover .navbar-nav .show > .nav-link,
.navbar-hover-light:hover .navbar-nav .active > .nav-link,
.navbar-hover-light:hover .navbar-nav .nav-link.show,
.navbar-hover-light:hover .navbar-nav .nav-link.active,
.navbar-fixed-light.fixed-top .navbar-nav .show > .nav-link,
.navbar-fixed-light.fixed-top .navbar-nav .active > .nav-link,
.navbar-fixed-light.fixed-top .navbar-nav .nav-link.show,
.navbar-fixed-light.fixed-top .navbar-nav .nav-link.active {
  color: white;
}

.navbar-light .navbar-nav .nav-link:hover,
.navbar-light .navbar-nav .nav-link:focus,
.navbar-hover-light:hover .navbar-nav .nav-link:hover,
.navbar-hover-light:hover .navbar-nav .nav-link:focus,
.navbar-fixed-light.fixed-top .navbar-nav .nav-link:hover,
.navbar-fixed-light.fixed-top .navbar-nav .nav-link:focus {
  color: rgba(255, 255, 255, 1);
}

.navbar-dark .dropdown-toggle::after,
.navbar-hover-dark:hover .dropdown-toggle::after,
.navbar-fixed-dark.fixed-top .dropdown-toggle::after {
  background: right center
    url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64' aria-labelledby='title' aria-describedby='desc' role='img' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3EAngle Down%3C/title%3E%3Cdesc%3EA line styled icon from Orion Icon Library.%3C/desc%3E%3Cpath data-name='layer1' fill='none' stroke='rgba(255,255,255,0.9)' stroke-miterlimit='10' stroke-width='5' d='M20 26l11.994 14L44 26' stroke-linejoin='round' stroke-linecap='round'%3E%3C/path%3E%3C/svg%3E")
    no-repeat !important;
}

.megamenu {
  min-width: 300px !important;
  width: fit-content !important;
  padding: 10px 10px !important;
}
.logoImg {
  width: 120px;
  margin: 10px 0;
}
.navbar {
  padding-left: 5.6rem !important;
  padding-right: 5.6rem !important;
}

@media (max-width: 1300px) {
  .navbar {
    padding-left: 3rem !important;
    padding-right: 3rem !important;
  }
}

@media (max-width: 991px) {
  .mobile {
    display: flex !important;
  }
  .desktop {
    display: none !important;
  }
  .navbar {
    padding-left: 0.5rem !important;
    padding-right: 0 !important;
    padding-top: 0rem !important;
    padding-bottom: 0rem !important;
  }
}
@media (max-width: 768px) {
  .megamenu {
    min-width: 400px !important;
  }

  .logoImg {
    width: 110px;
    margin: 12px 0 10px 0;
  }
}
</style>

<script>
import axios from "axios";
import currencyFormatter from "currency-formatter";
import { Result } from "postcss";

export default {
  name: "Header",
  data() {
    return {
      loggedIn: false,
      username: "",
      cart: [],
      total: 0,
      categories: [],
      filter: "",
      headerMessage: "",
      USDData: {},
      USDEnabled: null,
    };
  },
  beforeMount() {
    this.getShippingData();
    this.getUSDSettings();
    this.getCategories();
    const token = localStorage.getItem("token_shopuser");
    if (token === null) {
      this.loggedIn = false;
    } else {
      this.getCart();
      this.created();
      this.loggedIn = true;
      const username = JSON.parse(localStorage.getItem("data_shopuser"));
      this.username = username[0];
    }
  },
  methods: {
    toHome() {
      this.$router.push({ name: "home" });
    },
    toProducts() {
      this.$router.push({ name: "products" });
    },
    getShippingData() {
      axios
        .get(this.$url + "/getshippingdata", {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((response) => {
          const { data } = response;
          if (data[0]) {
            this.headerMessage = data[0].message;
          }
        })
        .catch((error) => {
          console.log(error.response.data.msg);
        });
    },
    redirectToSubcategory(subitem) {
      this.$router.push({
        name: "products",
        query: { category: subitem.categoryName, subcategory: subitem.name },
      });
    },
    search() {
      this.$router.push({
        name: "products",
        query: { filter: this.filter },
      });
    },
    getCategories() {
      axios
        .get(this.$url + "/public/getallcategories", {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((response) => {
          const { data } = response;
          this.categories = data;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    getCart() {
      const token = localStorage.getItem("token_shopuser");
      const getUser = JSON.parse(localStorage.getItem("data_shopuser"));
      const user = getUser[1];
      axios
        .get(this.$url + "/cart/get/" + user, {
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
        })
        .then((response) => {
          const { data } = response;
          this.total = 0;
          this.cart = data;
          for (const item of data) {
            const subtotal = item.product.price * item.amountOfProducts;
            this.total = this.total + subtotal;
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    priceConverter(price) {
      return currencyFormatter.format(price, { code: "ARS" });
    },
    logOut() {
      localStorage.removeItem("token_shopuser");
      localStorage.removeItem("data_shopuser");
      if (this.$route.path !== "/") {
        this.$router.push({ name: "home" });
      }
      window.location.reload();
    },

    created() {
      this.sockets.subscribe("listenCart", (data) => {
        this.getCart();
      });
    },
    deleteItem(id) {
      const token = localStorage.getItem("token_shopuser");
      axios
        .delete(this.$url + "/cart/delete/" + id, {
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
        })
        .then((response) => {
          const { data } = response;
          this.getCart();
          this.$socket.emit("sendCart", true);
        })
        .catch((error) => {
          this.msm_error = error.response.data.msg;
        });
    },
    getUSDSettings() {
      axios
        .get(`${this.$url}/public/getusdsettings`, {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((response) => {
          this.USDData = response.data[0];
          if (this.USDData.enabled === true) {
            this.USDEnabled = true;
          }
          if (this.USDData.enabled === false) {
            this.USDEnabled = false;
          }
        })
        .catch((error) => {
          console.log(error.response.data.msg);
        });
    },
  },
};
</script>
