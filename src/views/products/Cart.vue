<template>
  <div>
    <!-- Hero Section-->
    <section class="hero productMargin">
      <div class="container">
        <!-- Breadcrumbs -->
        <ol class="breadcrumb justify-content-center">
          <li class="breadcrumb-item">
            <router-link to="/">Inicio</router-link>
          </li>
          <li class="breadcrumb-item active">Carrito</li>
        </ol>
        <!-- Hero Content-->
        <div class="pb-5 text-center hero-content">
          <h1 class="hero-heading categorySize">Carrito de compras</h1>
          <div class="row">
            <div
              class="col-xl-8 offset-xl-2"
              v-if="cart.length === 0 || cart.length > 1"
            >
              <p class="lead text-muted">
                Tenés {{ cart.length }} productos en tu carrito de compras
              </p>
            </div>
            <div class="col-xl-8 offset-xl-2" v-if="cart.length === 1">
              <p class="lead text-muted">
                Tenés {{ cart.length }} producto en tu carrito de compras
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Shopping Cart Section-->
    <template v-if="loading">
      <div>
        <div class="row">
          <div class="text-center col-12">
            <div class="mt-5 mb-5 spinner-border" role="status">
              <span class="visually-hidden">Cargando...</span>
            </div>
          </div>
        </div>
      </div>
    </template>
    <template v-if="!loading">
      <section style="margin-bottom: 170px">
        <div class="container">
          <div class="mb-5 row" v-if="cart.length >= 1">
            <div class="col-lg-8">
              <div class="cart">
                <div class="cart-wrapper">
                  <div
                    class="text-center cart-header"
                    style="
                      border-bottom: 1px solid #1c4c3b;
                      background: transparent;
                    "
                  >
                    <div class="row">
                      <div class="col-5">Producto</div>
                      <div class="col-2">Precio</div>
                      <div class="col-2">Cantidad</div>
                      <div class="col-2">Subtotal</div>
                      <div class="col-1"></div>
                    </div>
                  </div>
                  <div class="cart-body">
                    <!-- Product-->
                    <div
                      v-if="cart.length > 0"
                      class="cart-item"
                      v-for="item in cart"
                    >
                      <div class="text-center row d-flex align-items-center">
                        <div class="col-5">
                          <div class="d-flex align-items-center">
                            <router-link :to="/product/ + item.product.slug">
                              <img
                                class="cart-item-img"
                                :src="item.product.image"
                                alt="..."
                              />
                            </router-link>

                            <div class="cart-title text-start">
                              <router-link
                                :to="/product/ + item.product.slug"
                                class="text-uppercase text-dark"
                                style="letter-spacing: 0.5px"
                                ><strong>{{ item.product.name }}</strong>
                              </router-link>
                              <br />
                              <span
                                style="
                                  margin-top: 3px;
                                  font-weight: 500;
                                  font-size: 13px;
                                "
                                v-if="item.variant"
                                >{{ item.product.str_variant }}:
                                {{ item.variant.variant }}
                              </span>
                              <!-- <span class="text-sm text-muted">{{item.product.str_variant}}: {{item.variant.variant}}</span> -->
                            </div>
                          </div>
                        </div>

                        <div class="col-2" v-if="USDEnabled == false">
                          {{
                            priceConverter(item.product.price * USDData.value)
                          }}
                        </div>
                        <div class="col-2" v-if="USDEnabled == true">
                          {{ priceConverter(item.product.price) }}
                        </div>

                        <div class="col-2">
                          <div
                            class="d-flex align-items-center"
                            style="width: 100px; justify-content: center"
                          >
                            <span class="" type="text">{{
                              item.amountOfProducts
                            }}</span>
                          </div>
                        </div>

                        <div
                          class="text-center col-2"
                          v-if="USDEnabled == false"
                        >
                          {{
                            priceConverter(
                              item.product.price *
                                USDData.value *
                                item.amountOfProducts
                            )
                          }}
                        </div>
                        <div
                          class="text-center col-2"
                          v-if="USDEnabled == true"
                        >
                          {{
                            priceConverter(
                              item.product.price * item.amountOfProducts
                            )
                          }}
                        </div>

                        <div class="text-center col-1">
                          <a
                            class="cart-remove"
                            v-on:click="deleteItem(item._id)"
                          >
                            <img
                              src="/assets/icons/redclose.png"
                              alt=""
                              style="width: 12px; height: 12px"
                            />
                          </a>
                        </div>
                      </div>
                    </div>
                    <!-- Product-->
                  </div>
                </div>
              </div>
              <div
                class="my-5 d-flex justify-content-between flex-column flex-lg-row"
              >
                <router-link
                  to="/products"
                  class="btn btn-link"
                  style="letter-spacing: 0px !important; color: black"
                  >Continuar comprando</router-link
                >
              </div>
            </div>
            <div class="col-lg-4">
              <div class="block mb-5">
                <div class="block-header" style="background-color: transparent">
                  <h6 class="mb-0 text-uppercase">Resumen del pedido</h6>
                </div>
                <div class="pt-1 block-body">
                  <ul class="mb-0 order-summary list-unstyled">
                    <li class="border-0 order-summary-item">
                      <span>Subtotal sin envío</span>
                      <strong
                        class="order-summary-total"
                        v-if="USDEnabled == false"
                        >{{ priceConverter(total * USDData.value) }}</strong
                      >
                      <strong
                        class="order-summary-total"
                        v-if="USDEnabled == true"
                        >{{ priceConverter(total) }}</strong
                      >
                    </li>
                  </ul>
                </div>
                <router-link
                  v-if="cart.length >= 1"
                  class="btn btn-dark btnAdd"
                  to="/checkout"
                  style="
                    margin: 0 1.5rem;
                    font-size: 12px;
                    letter-spacing: 1px;
                    font-weight: 800;
                  "
                  >Realizar compra</router-link
                >
              </div>
            </div>
          </div>

          <div
            class="col-lg-8 col-xl-9"
            v-if="cart.length === 0"
            style="margin: 0 auto; margin-bottom: 500px"
          >
            <div class="card" style="">
              <div class="card-body">
                <div class="row">
                  <div class="text-center col-12">
                    <img
                      src="../../../public/assets/icons/cart0.png"
                      style="width: 90px; height: 90px; margin-bottom: 35px"
                      alt=""
                    />
                    <h3 style="font-size: 24px">
                      No tenés productos en tu carrito.
                    </h3>
                    <span
                      style="color: black; font-weight: 400; font-size: 17px"
                      >¿Que esperas para llenarlo?
                    </span>
                    <router-link
                      to="/products"
                      class="textLink"
                      style="
                        font-weight: 600;
                        font-size: 17px;
                        margin-left: 1px !important;
                      "
                      >Ver productos</router-link
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </template>
  </div>
</template>

<script>
import axios from "axios";
import currencyFormatter from "currency-formatter";

export default {
  name: "Cart",
  data() {
    return {
      cart: [],
      loading: true,
      total: 0,
      USDData: {},
      USDEnabled: null,
    };
  },
  beforeMount() {
    this.getUSDSettings();
    this.getCart();
  },
  mounted() {
    window.scrollTo(0, 0);
  },
  methods: {
    getCart() {
      const token = localStorage.getItem("token_shopuser");
      if (token) {
        var loader = this.$loading.show({
          container: this.fullPage ? null : this.$refs.formContainer,
          canCancel: false,
          color: "#1c4c3b",
          opacity: 1,
        });
      }
      if (!token) {
        this.loading = false;
      }

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
          this.total = 0;
          const { data } = response;
          this.cart = data;
          this.loading = false;
          loader.hide();
          for (const item of data) {
            const subtotal = item.product.price * item.amountOfProducts;
            this.total = this.total + subtotal;
          }
        })
        .catch((error) => {
          console.log(error);
          loader.hide();
        });
    },
    priceConverter(price) {
      return currencyFormatter.format(price, { code: "ARS" });
    },
    deleteItem(id) {
      this.loading = true;

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
          this.loading = false;
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
