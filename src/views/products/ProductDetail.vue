<template>
  <div style="background: white" class="pb-5">
    <div class="notificationContainer" v-bind:class="{ actived: added }">
      <div
        style="
          display: flex;
          justify-content: center;
          height: 70%;
          align-items: center;
          gap: 12px;
        "
      >
        <img src="@/assets/correct.png" alt="" style="width: 35px" />
        <span>Agregaste {{ product[0].name }} a tu carrito</span>
      </div>
    </div>

    <section class="product-details marginFix">
      <div class="container">
        <div class="row">
          <div class="pt-4 order-0 col-lg-7 order-lg-1">
            <div class="row">
              <div
                class="d-none d-md-block col-md-2 pe-0"
                style="width: 10% !important"
              >
                <div class="owl-thumbs" data-slider-id="1">
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="product[0]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="product[0].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[0]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[0].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[1]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[1].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[2]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[2].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[3]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[3].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[4]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[4].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[5]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[5].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[6]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[6].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[7]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[7].image"
                    />
                  </button>
                  <button
                    class="mb-3 owl-thumb-item detail-thumb-item"
                    v-if="gallery[8]"
                  >
                    <img
                      class="img-fluid productBorderRadius"
                      :src="gallery[8].image"
                    />
                  </button>
                </div>
              </div>
              <div class="col-12 col-md-10 detail-carousel">
                <div v-if="product[0].discount" class="ribbon ribbon-primary">
                  Oferta
                </div>

                <div
                  class="owl-carousel detail-slider owl-theme owl-dots-modern"
                  data-slider-id="1"
                >
                  <div class="item" v-if="product[0].image">
                    <a
                      class="glightbox"
                      :src="product[0].image"
                      :href="product[0].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="product[0].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[0]">
                    <a
                      class="glightbox"
                      :src="gallery[0].image"
                      :href="gallery[0].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[0].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[1]">
                    <a
                      class="glightbox"
                      :src="gallery[1].image"
                      :href="gallery[1].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[1].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[2]">
                    <a
                      class="glightbox"
                      :src="gallery[2].image"
                      :href="gallery[2].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[2].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[3]">
                    <a
                      class="glightbox"
                      :src="gallery[3].image"
                      :href="gallery[3].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[3].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[4]">
                    <a
                      class="glightbox"
                      :src="gallery[4].image"
                      :href="gallery[4].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[4].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[5]">
                    <a
                      class="glightbox"
                      :src="gallery[5].image"
                      :href="gallery[5].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[5].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[6]">
                    <a
                      class="glightbox"
                      :src="gallery[6].image"
                      :href="gallery[6].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[6].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[7]">
                    <a
                      class="glightbox"
                      :src="gallery[7].image"
                      :href="gallery[7].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[7].image"
                        alt="..."
                      />
                    </a>
                  </div>
                  <div class="item" v-if="gallery[8]">
                    <a
                      class="glightbox"
                      :src="gallery[8].image"
                      :href="gallery[8].image"
                      data-gallery="product-gallery"
                    >
                      <img
                        class="img-fluid"
                        :src="gallery[8].image"
                        alt="..."
                      />
                    </a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="order-1 col-lg-5 ps-lg-4 order-lg-2">
            <ul class="breadcrumb undefined">
              <li class="breadcrumb-item">
                <router-link to="/">Inicio</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link
                  :to="{
                    name: 'products',
                    query: { category: product[0].category },
                  }"
                  >{{ product[0].category }}</router-link
                >
              </li>
              <li class="breadcrumb-item">
                <router-link
                  :to="{
                    name: 'products',
                    query: {
                      category: product[0].category,
                      subcategory: product[0].subcategory,
                    },
                  }"
                  >{{ product[0].subcategory }}</router-link
                >
              </li>
              <li class="breadcrumb-item active">{{ product[0].name }}</li>
            </ul>
            <h1 class="mb-4 productName">{{ product[0].name }}</h1>
            <div
              class="mb-4 d-flex flex-column flex-sm-row align-items-sm-center justify-content-sm-between"
            >
              <ul class="mb-2 list-inline mb-sm-0">
                <li
                  class="mb-0 list-inline-item h3 fw-normal"
                  v-if="USDEnabled == false"
                >
                  AR{{ priceConverter(product[0].price * USDData.value) }}
                </li>
                <li
                  class="mb-0 list-inline-item h3 fw-normal"
                  v-if="USDEnabled == true"
                >
                  AR{{ priceConverter(product[0].price) }}
                </li>
                <li class="list-inline-item text-muted fw-light">
                  <del v-if="product[0].discount">{{
                    priceConverter(product[0].price + 5999)
                  }}</del>
                </li>
              </ul>
            </div>
            <p class="mb-4 text-muted">{{ product[0].description }}</p>

            <div class="row">
              <div
                v-if="product[0].hasVariant"
                class="mb-3 col-sm-6 col-lg-12 detail-option"
              >
                <h6 class="detail-option-heading">
                  {{ product[0].str_variant }}
                </h6>
                <div style="display: flex; flex-direction: row; gap: 10px">
                  <template v-for="variant in variants">
                    <div
                      v-if="variant.stock > 0"
                      style="width: fit-content; padding: 0 10px"
                      class="hoverClass"
                      v-on:click="getVariant(variant._id)"
                      :id="'variant_' + variant._id"
                    >
                      <input
                        class="input-invisible"
                        type="radio"
                        :value="variant._id"
                        name="size"
                        value="value_0"
                        id="size_0"
                        required
                      />
                      <span
                        v-on:click="getVariant(variant._id)"
                        :for="'variant_' + variant._id"
                        style="user-select: none"
                        >{{ variant.variant }}
                      </span>
                    </div>
                  </template>
                </div>
              </div>

              <div class="mb-4 col-12 col-lg-6 detail-option">
                <label class="detail-option-heading fw-bold">Cantidad</label>
                <input
                  class="form-control detail-quantity"
                  v-model="cartObj.amountOfProducts"
                  name="items"
                  type="number"
                  style="
                    border-radius: 8px;
                    border: 1px solid rgb(0 0 0/ 20%);
                    width: 140px !important;
                  "
                />
              </div>
            </div>

            <!-- ERROR ALERT -->
            <div
              class="alert"
              style="
                width: fit-content !important;
                height: fit-content !important;
                padding: 7px 14px;
                display: flex !important;
                justify-content: left !important;
                border-radius: 8px;
                margin: 0 0 !important;
                margin-bottom: 25px !important;
              "
              v-if="!valid"
            >
              <small class="">{{ msm_error }} </small>
            </div>

            <ul
              class="list-inline"
              style="
                min-width: 260px;
                width: fit-content;
                min-height: 50px;
                height: fit-content;
              "
            >
              <template v-if="addedToCart">
                <div>
                  <div class="row">
                    <div class="text-center col-12">
                      <div class="mt-4 mb-5 spinner-border" role="status">
                        <span class="visually-hidden">Cargando...</span>
                      </div>
                    </div>
                  </div>
                </div>
              </template>

              <li class="list-inline-item">
                <button
                  v-if="!addedToCart"
                  class="mb-1 btn btn-dark btn-md btnAdd"
                  type="button"
                  v-on:click="addToCart()"
                  style="font-size: 12px; letter-spacing: 1px; font-weight: 800"
                >
                  AGREGAR AL CARRITO
                </button>
              </li>
              <!-- <li class="list-inline-item"><a class="mb-1 btn btn-outline-secondary" href="#"> <i class="far fa-heart me-2"></i>Add to wishlist</a></li> -->
            </ul>
          </div>
        </div>
      </div>
    </section>
    <section class="mt-5">
      <div class="container">
        <ul class="nav nav-tabs flex-column flex-sm-row" role="tablist">
          <li class="nav-item">
            <a
              class="active nav-link detail-nav-link"
              data-bs-toggle="tab"
              href="#additional-information"
              role="tab"
              >Información del producto</a
            >
          </li>
        </ul>
        <div class="py-4 tab-content">
          <div
            class="tab-pane active"
            id="additional-information"
            role="tabpanel"
          >
            <div class="row">
              <div class="col-lg-6">
                <table class="table text-sm">
                  <tbody>
                    <tr>
                      <th class="border-0 text-uppercase fw-normal">
                        Producto
                      </th>
                      <td class="border-0 text-muted">{{ product[0].name }}</td>
                    </tr>
                    <tr>
                      <th class="text-uppercase fw-normal">Categoría</th>
                      <td class="text-muted">{{ product[0].category }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <div class="col-lg-6">
                <table class="table text-sm">
                  <tbody>
                    <tr>
                      <th class="border-0 text-uppercase fw-normal">
                        En descuento
                      </th>
                      <td
                        class="border-0 text-muted"
                        v-if="product[0].discount"
                      >
                        Si
                      </td>
                      <td
                        class="border-0 text-muted"
                        v-if="!product[0].discount"
                      >
                        No
                      </td>
                    </tr>
                    <tr>
                      <th class="text-uppercase fw-normal">Categoría</th>
                      <td class="text-muted">{{ product[0].category }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="my-5">
      <div class="container">
        <header class="text-center">
          <h6
            class="mb-5 text-uppercase"
            style="color: #1c4c3b; letter-spacing: 1px; font-size: 20px"
          >
            Tal vez te guste
          </h6>
        </header>
        <div class="row">
          <!-- product-->
          <div
            class="col-lg-2 col-md-4 col-6"
            v-for="product in relatedProducts.products"
          >
            <div v-on:click="goTo(product.slug)">
              <div class="product">
                <div class="product-image" style="height: 200px">
                  <div class="ribbon ribbon-info" v-if="product.discount">
                    En oferta
                  </div>
                  <img class="img-fluid" :src="product.image" alt="product" />
                  <div class="product-hover-overlay" style="border-radius: 4px">
                    <div
                      class="product-hover-overlay-buttons"
                      style="border-radius: 4px"
                    >
                      <a
                        class="btn btn-dark btn-buy"
                        style="background-color: #1c4c3b; border-radius: 4px"
                        href=""
                        ><span
                          class="btn-buy-label"
                          style="font-size: 11px; letter-spacing: 1px"
                          >Ver más</span
                        ></a
                      >
                    </div>
                  </div>
                </div>
                <div class="py-2">
                  <p class="mb-1 text-sm text-muted">
                    {{ product.subcategory }}
                  </p>
                  <h3 class="mb-1 h6 text-uppercase">
                    <a class="text-dark" style="cursor: pointer">{{
                      product.name
                    }}</a>
                  </h3>
                  <span v-if="USDEnabled == true" class="text-muted"
                    >AR{{ priceConverter(product.price) }}
                  </span>
                  <span v-if="USDEnabled == false" class="text-muted"
                    >AR{{ priceConverter(product.price * USDData.value) }}
                  </span>
                </div>
              </div>
            </div>
          </div>
          <!-- /product-->
        </div>
      </div>
    </section>
  </div>
</template>

<style>
.bgVariant {
  color: white;
  background-color: #1c4c3b;
  border: 1px solid #1c4c3b;
}

.productName {
  font-size: 44px;
}

.owl-carousel .owl-stage-outer {
  max-height: 70vh !important;
}

.owl-theme.owl-dots-modern .owl-dots .owl-dot.active span {
  background-color: #1c4c3b !important;
}

@media (max-width: 991px) {
  .productName {
    font-size: 36px;
  }
}
</style>

<script>
import axios from "axios";
import { initCarousel } from "../../../public/assets/js/theme.d7b4a888.js";
import currencyFormatter from "currency-formatter";
import $ from "jquery";

export default {
  name: "ProductDetail",
  data() {
    return {
      product: [],
      gallery: [],
      variants: [],
      relatedProducts: [],
      cartObj: {
        amountOfProducts: 1,
      },
      userData: {},
      msm_error: "",
      valid: true,
      added: false,
      addedToCart: false,
      USDData: {},
      USDEnabled: null,
    };
  },
  beforeMount() {
    this.getUSDSettings();
    this.getProductData();
    initCarousel.initGallery();
    initCarousel.initGlight();
  },
  mounted() {
    window.scrollTo(0, 0);
  },
  methods: {
    goTo(product) {
      this.$router.push({
        path: `/product/${product}`,
      });
      window.location.reload();
      window.scrollTo(0, 0);
    },
    getProductData() {
      var loader = this.$loading.show({
        container: this.fullPage ? null : this.$refs.formContainer,
        canCancel: false,
        color: "#1c4c3b",
        opacity: 1,
      });
      axios
        .get(this.$url + "/public/getoneproduct/" + this.$route.params.slug, {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((response) => {
          const { data } = response;
          this.product = data.product;
          this.gallery = data.gallery;
          this.variants = data.variants;

          loader.hide();
          initCarousel.initGallery();
          initCarousel.initGlight();
          this.getRelatedProducts(this.product[0].category);
          const user = JSON.parse(localStorage.getItem("data_shopuser"));
          this.userData = user;
          this.cartObj.product = this.product[0]._id;
          this.cartObj.client = this.userData[1];
          // CALL FUNCTION TO MULTIPLY PRICE x USD//
        })
        .catch((error) => {
          loader.hide();
          this.msm_error = error.response.data.msg;
        });
    },
    priceConverter(price) {
      return currencyFormatter.format(price, { code: "ARS" });
    },
    getRelatedProducts(category) {
      axios
        .get(this.$url + "/public/getrelatedproducts/" + category, {
          headers: {
            "Content-Type": "application/json",
          },
        })
        .then((response) => {
          const { data } = response;
          this.relatedProducts = data;
        })
        .catch((error) => {
          console.log(error.response.data.msg);
          this.msm_error = error.response.data.msg;
        });
    },
    getVariant(id) {
      this.cartObj.variant = id;
      setTimeout(() => {
        $(".hoverClass").removeClass("bgVariant");
        $("#variant_" + id).addClass("bgVariant");
      }, 40);
    },
    addToCart() {
      this.addedToCart = true;
      const loggedIn = localStorage.getItem("token_shopuser");
      if (!loggedIn) {
        this.valid = false;
        this.addedToCart = false;
        this.msm_error = "Iniciá sesión para comprar";
        return;
      }

      if (this.product[0].hasVariant && !this.cartObj.variant) {
        this.valid = false;
        this.addedToCart = false;
        return (this.msm_error = "Selecciona una variante de producto");
      }
      const token = localStorage.getItem("token_shopuser");
      axios
        .post(this.$url + "/cart/create", this.cartObj, {
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
        })
        .then((response) => {
          this.$socket.emit("sendCart", true);
          const { data } = response;
          if (data.msg === "No hay suficiente stock.") {
            this.valid = false;
            this.addedToCart = false;
            this.msm_error = data.msg;
            return;
          }
          this.valid = true;
          this.msm_error = "";
          this.added = true;
          this.addedToCart = false;
          setTimeout(() => {
            this.added = false;
          }, 4000);
        })
        .catch((error) => {
          console.log(error.response.data.msg);
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
