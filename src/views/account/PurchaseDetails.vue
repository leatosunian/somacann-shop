<template>
  <div>
    <section class="hero productMargin">
      <div class="container">
        <!-- Breadcrumbs -->
        <ol class="breadcrumb justify-content-center">
          <li class="breadcrumb-item">
            <router-link to="/">Inicio</router-link>
          </li>
          <li class="breadcrumb-item">Mi perfil</li>
          <li class="breadcrumb-item active">Mis pedidos</li>
        </ol>
        <!-- Hero Content-->
        <div class="pb-5 text-center hero-content">
          <h1 class="hero-heading categorySize">
            Pedido #{{ saleData.orderNumber }}
          </h1>
          <div class="row">
            <div class="col-xl-8 offset-xl-2">
              <p class="lead text-muted">
                Estamos preparando tu pedido #{{
                  saleData.orderNumber
                }}
                realizado el {{ saleData.day }}/{{ saleData.month }}/{{
                  saleData.year
                }}. Al ser despachado en el correo, el código de seguimiento
                será mostrado en los datos de envío debajo. Si tenés algún
                inconveniente con tu compra,
                <a href="https://api.whatsapp.com/send?phone=5492235892260"
                  >contactanos</a
                >
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-xl-9">
            <div class="cart">
              <div class="cart-wrapper">
                <div class="text-center cart-header">
                  <div class="row">
                    <div class="col-6">Producto</div>
                    <div class="col-2">Precio</div>
                    <div class="col-2">Cantidad</div>
                    <div class="col-2">Subtotal</div>
                  </div>
                </div>
                <div class="cart-body">
                  <!-- Product-->
                  <div
                    class="cart-item"
                    v-if="products != null"
                    v-for="item in products"
                  >
                    <div class="text-center row d-flex align-items-center">
                      <div class="col-6">
                        <div class="d-flex align-items-center">
                          <router-link :to="/product/ + item.product.slug">
                            <img
                              class="cart-item-img"
                              :src="item.product.image"
                              alt="..."
                            />
                          </router-link>
                          <div class="cart-title text-start">
                            <a
                              class="text-uppercase text-dark"
                              href="detail.html"
                              ><strong>{{ item.product.name }}</strong>
                            </a>
                            <br />
                            <!-- <span class="text-sm text-muted">{{item.product.str_variant
                                }}: {{item.variant.variant}}</span> -->
                          </div>
                        </div>
                      </div>
                      <div v-if="USDEnabled === false" class="col-2">
                        {{ priceConverter(item.unitPrice * USDData.value) }}
                      </div>
                      <div v-if="USDEnabled === true" class="col-2">
                        {{ priceConverter(item.unitPrice) }}
                      </div>
                      <div class="col-2">
                        {{ item.items }}
                      </div>
                      <div
                        v-if="USDEnabled === false"
                        class="text-center col-2"
                      >
                        {{
                          priceConverter(
                            item.unitPrice * item.items * USDData.value
                          )
                        }}
                      </div>
                      <div v-if="USDEnabled === true" class="text-center col-2">
                        {{ priceConverter(item.unitPrice * item.items) }}
                      </div>
                    </div>
                  </div>
                  <!-- Product-->
                </div>
              </div>
            </div>
            <div class="my-5 row">
              <div class="col-md-6">
                <div class="block mb-5">
                  <div class="block-header">
                    <h6 class="mb-0 text-uppercase">Resumen del pedido</h6>
                  </div>
                  <div class="pt-1 block-body bg-light">
                    <ul class="mb-0 order-summary list-unstyled">
                      <li class="order-summary-item">
                        <span>Subtotal </span
                        ><span>{{ priceConverter(saleData.total) }}</span>
                      </li>
                      <li class="order-summary-item">
                        <span>Envío</span
                        ><span>{{
                          priceConverter(saleData.shippingPrice)
                        }}</span>
                      </li>
                      <li class="border-0 order-summary-item">
                        <span>Total</span
                        ><strong class="order-summary-total">{{
                          priceConverter(
                            saleData.total + saleData.shippingPrice
                          )
                        }}</strong>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>

              <div class="col-md-6">
                <div class="block-header">
                  <h6 class="mb-0 text-uppercase">Datos de envío</h6>
                </div>
                <div class="pt-1 block-body bg-light" v-if="address.name">
                  <p>
                    <strong>Destinatario</strong>: {{ address.surname }},
                    {{ address.name }}
                    <br />
                    <strong>Domicilio</strong>: {{ address.address }}
                    <br />
                    <strong>Provincia</strong>: {{ address.province }}
                    <br />
                    <strong>Ciudad</strong>: {{ address.city }}
                    <br />
                    <strong>Código postal</strong>: {{ address.code }}
                    <br />
                    <strong>País</strong>: {{ address.country }}
                    <br />
                    <strong>Estado</strong>:
                    <span style="color: black; font-weight: 800">{{
                      saleData.statusStr
                    }}</span>
                    <br />
                    <strong v-if="saleData.trackingCode"
                      >Código de seguimiento:</strong
                    >
                    <a
                      target="_blank"
                      :href="
                        'https://www.andreani.com/#!/informacionEnvio/' +
                        saleData.trackingCode
                      "
                      >{{ saleData.trackingCode }}</a
                    >
                    <br />
                  </p>
                </div>

                <div class="pt-1 block-body bg-light" v-if="!address.name">
                  <p>
                    <strong>Tipo de envío</strong>: retiro por sucursal del
                    vendedor
                    <br />
                  </p>
                </div>
              </div>
            </div>
          </div>
          <!-- Customer Sidebar-->
          <div class="mb-5 col-xl-3 col-lg-4">
            <AccountSidebar />
          </div>
          <!-- /Customer Sidebar-->
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import currencyFormatter from "currency-formatter";
import AccountSidebar from "@/components/AccountSidebar.vue";

export default {
  name: "PurchaseDetails",
  components: {
    AccountSidebar,
  },
  data() {
    return {
      products: [],
      address: {},
      saleData: {},
      USDData: {},
      USDEnabled: null,
    };
  },
  mounted() {
    window.scrollTo(0, 0);
  },
  beforeMount() {
    this.getPurchaseData();
    this.getUSDSettings();
  },
  methods: {
    priceConverter(price) {
      return currencyFormatter.format(price, { code: "ARS" });
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
    getPurchaseData() {
      var loader = this.$loading.show({
        container: this.fullPage ? null : this.$refs.formContainer,
        canCancel: false,
        color: "#1c4c3b",
        opacity: 1,
      });
      if (this.$route.params.id.length < 15) {
        loader.hide();
        return;
      }
      const token = localStorage.getItem("token_shopuser");
      axios
        .get(this.$url + "/profile/order/" + this.$route.params.id, {
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
        })
        .then((response) => {
          const { data } = response;
          if (data.sale[0].address) {
            this.address = data.sale[0].address;
          }
          this.saleData = data.sale[0];
          this.products = data.saleDetails;
          loader.hide();
        })
        .catch((error) => {
          loader.hide();
        });
    },
  },
};
</script>
