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
          <li class="breadcrumb-item">Tienda</li>
          <li
            class="breadcrumb-item"
            v-if="this.$route.query.category && this.$route.query.subcategory"
          >
            <span>{{ this.$route.query.category }}</span>
          </li>
          <li
            class="breadcrumb-item active"
            v-if="this.$route.query.category && !this.$route.query.subcategory"
          >
            <span>{{ this.$route.query.category }}</span>
          </li>
          <li
            class="breadcrumb-item active"
            v-if="this.$route.query.category && this.$route.query.subcategory"
          >
            <span>{{ this.$route.query.subcategory }}</span>
          </li>
        </ol>
        <!-- Hero Content-->
        <div class="text-center marginProducts hero-content">
          <h2
            class="hero-heading categorySize"
            v-if="this.$route.query.category"
          >
            {{ this.$route.query.category }}
          </h2>
          <p
            class="hero-heading subcatSize"
            v-if="this.$route.query.subcategory"
          >
            {{ this.$route.query.subcategory }}
          </p>
          <h2
            class="hero-heading categorySize"
            v-if="!this.$route.query.category && !this.$route.query.subcategory"
          >
            Todos los productos
          </h2>
          <!-- <div class="row">
            <div class="col-xl-8 offset-xl-2">
              <p class="lead text-muted">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
                eiusmod tempor incididunt.
              </p>
            </div>
          </div> -->
        </div>
      </div>
    </section>
    <div class="container">
      <div class="row">
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
          <!-- Grid -->
          <div
            class="products-grid col-xl-9 col-lg-8 order-lg-2"
            style="margin-bottom: 100px"
          >
            <header class="product-grid-header">
              <div class="mb-3 me-3">
                Mostrando <strong>1-12 </strong>de
                <strong>{{ allProducts.length }} </strong>productos
              </div>
              <div class="mb-3 me-3">
                <span class="me-2">Mostrar</span
                ><a
                  class="product-grid-header-show"
                  style="cursor: pointer"
                  v-bind:class="{ active: perPage === 12 }"
                  v-on:click="showPerPage(12)"
                  >12 </a
                ><a
                  class="product-grid-header-show"
                  style="cursor: pointer"
                  v-bind:class="{ active: perPage === 21 }"
                  v-on:click="showPerPage(21)"
                  >21
                </a>
              </div>
              <div class="mb-3 d-flex align-items-center">
                <span class="d-inline-block me-2">Filtrar por</span>
                <select
                  class="w-auto border-0 form-select"
                  v-model="sortBy"
                  v-on:change="setSortBy()"
                >
                  <option value="Por defecto" selected>Por defecto</option>
                  <option value="Mayor a menor precio">
                    Mayor a menor precio
                  </option>
                  <option value="Menor a mayor precio">
                    Menor a mayor precio
                  </option>
                </select>
              </div>
            </header>
            <div v-if="itemsForList.length > 0" class="row" id="my-table">
              <!-- product-->
              <div class="col-xl-4 col-6" v-for="item in itemsForList">
                <router-link :to="/product/ + item.slug">
                  <div class="product">
                    <div class="product-image" style="border: none !important">
                      <div class="ribbon ribbon-info" v-if="item.discount">
                        En oferta
                      </div>
                      <img
                        class="img-fluid productBorderRadius"
                        :src="item.image"
                        alt="product"
                      />
                      <div
                        class="product-hover-overlay"
                        style="border-radius: 4px"
                      >
                        <div
                          class="product-hover-overlay-buttons"
                          style="border-radius: 4px"
                        >
                          <a
                            class="btn btn-dark btn-buy"
                            style="
                              background-color: #1c4c3b;
                              border-radius: 4px;
                            "
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
                      <p class="mb-1 text-sm text-muted">{{ item.category }}</p>
                      <h3
                        class="mb-1 h6"
                        style="
                          text-overflow: ellipsis;
                          overflow: hidden;
                          white-space: nowrap;
                          text-transform: uppercase;
                        "
                      >
                        <a class="text-dark" href="detail.html"
                          >{{ item.name }}
                        </a>
                      </h3>
                      <span class="text-muted" v-if="USDEnabled == false"
                        >AR{{
                          priceConverter(item.price * USDData.value)
                        }}</span
                      >
                      <span class="text-muted" v-if="USDEnabled == true"
                        >AR{{ priceConverter(item.price) }}</span
                      >
                    </div>
                  </div>
                </router-link>
              </div>
              <!-- /product-->
            </div>

            <div
              v-if="itemsForList.length === 0"
              class="row"
              style="padding: 140px 0"
              id="my-table"
            >
              <div class="card">
                <div class="card-body">
                  <div class="row">
                    <div class="text-center col-12">
                      <h3 style="font-size: 34px">
                        No se encontraron productos.
                      </h3>
                      <router-link
                        to="/products"
                        class="textLink"
                        style="
                          color: #1c4c3b !important;
                          font-weight: 600;
                          font-size: 17px;
                          margin-left: 1px !important;
                        "
                        >Ver todos los productos</router-link
                      >
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Pagination-->
            <b-pagination
              v-if="itemsForList.length > 0"
              v-model="currentPage"
              :total-rows="allProducts.length"
              :per-page="perPage"
              pills
              aria-controls="my-table"
              style="justify-content: center; color: black; margin-top: 25px"
              v-on:click="scrollToTop()"
            ></b-pagination>
          </div>
          <!-- / Grid End-->
        </template>

        <!-- Sidebar-->
        <div class="sidebar col-xl-3 col-lg-4 order-lg-1">
          <div class="px-3 sidebar-block px-lg-0 me-lg-4">
            <a
              class="d-lg-none block-toggler"
              data-bs-toggle="collapse"
              href="#categoriesMenu"
              aria-expanded="false"
              aria-controls="categoriesMenu"
              >Categorias</a
            >
            <div class="expand-lg collapse" id="categoriesMenu">
              <div class="mt-4 nav nav-pills flex-column mt-lg-0" role="menu">
                <template v-for="item in categories">
                  <div>
                    <template v-if="item.category._id == activeCat">
                      <div>
                        <div class="mb-2 sidebar-menu-item">
                          <a class="nav-link active" href="#!">
                            <div class="row">
                              <div class="col">
                                <a style="cursor: pointer">{{
                                  item.category.name
                                }}</a>
                              </div>
                              <div
                                data-bs-toggle="collapse"
                                :data-bs-target="
                                  '#subcategories' + item.category._id
                                "
                                aria-expanded="false"
                                :aria-controls="
                                  'subcategories' + item.category._id
                                "
                                role="menuitem"
                                class="col"
                                style="text-align: right"
                              >
                                <img
                                  src="assets/down-arrow-white.png"
                                  alt=""
                                  style="width: 15px"
                                />
                              </div>
                            </div>
                          </a>
                        </div>

                        <div
                          class="collapse"
                          :id="'subcategories' + item.category._id"
                        >
                          <div class="nav nav-pills flex-column ms-3">
                            <a
                              style="cursor: pointer"
                              class="mb-2 nav-link"
                              v-bind:class="{
                                subcatActive: subItem.name == activeSubcat,
                              }"
                              v-for="subItem in item.subcategories"
                              v-on:click="redirectToSubcategory(subItem, item)"
                              >{{ subItem.name }}</a
                            >
                          </div>
                        </div>
                      </div>
                    </template>

                    <template v-if="item.category._id !== activeCat">
                      <div>
                        <div class="mb-2 sidebar-menu-item">
                          <a class="nav-link">
                            <div class="row">
                              <div class="col">
                                <a
                                  v-on:click="redirectToCategory(item.category)"
                                  style="cursor: pointer"
                                >
                                  {{ item.category.name }}
                                </a>
                              </div>

                              <div
                                data-bs-toggle="collapse"
                                :data-bs-target="
                                  '#subcategories' + item.category._id
                                "
                                aria-expanded="false"
                                :aria-controls="
                                  'subcategories' + item.category._id
                                "
                                role="menuitem"
                                class="col"
                                style="text-align: right !important"
                              >
                                <img
                                  src="/assets/down-arrow.png"
                                  style="width: 12px"
                                  alt=""
                                />
                              </div>
                            </div>
                          </a>
                        </div>
                        <div
                          class="collapse"
                          :id="'subcategories' + item.category._id"
                        >
                          <div class="nav nav-pills flex-column ms-3">
                            <a
                              style="cursor: pointer"
                              class="mb-2 nav-link"
                              v-for="subItem in item.subcategories"
                              v-on:click="redirectToSubcategory(subItem, item)"
                              >{{ subItem.name }}</a
                            >
                          </div>
                        </div>
                      </div>
                    </template>
                  </div>
                </template>
              </div>
            </div>
          </div>

          <!-- PRICE FILTER -->
          <div class="px-3 sidebar-block px-lg-0 me-lg-4">
            <a
              class="d-lg-none block-toggler"
              data-bs-toggle="collapse"
              href="#priceFilterMenu"
              aria-expanded="false"
              aria-controls="priceFilterMenu"
              >Filtrar por precio</a
            >
            <div class="expand-lg collapse" id="priceFilterMenu">
              <h6 class="sidebar-heading d-none d-lg-block">
                Filtrar por precio
              </h6>
              <div
                class="mt-4 mt-lg-0"
                id="slider-snap"
                ref="priceSlider"
              ></div>
              <div class="nouislider-values">
                <div class="min">
                  Desde
                  <span id="slider-snap-value-lower"
                    >{{ priceConverter(minRange) }}
                  </span>
                </div>
                <div class="max">
                  Hasta
                  <span id="slider-snap-value-upper">{{
                    priceConverter(maxRange)
                  }}</span>
                </div>
                <input
                  class="slider-snap-input"
                  type="hidden"
                  name="pricefrom"
                  id="slider-snap-input-lower"
                  value="40"
                />
                <input
                  class="slider-snap-input"
                  type="hidden"
                  name="priceto"
                  id="slider-snap-input-upper"
                  value="110"
                />
              </div>
            </div>
          </div>

          <!-- <div class="px-3 sidebar-block px-lg-0 me-lg-4">
            <a
              class="d-lg-none block-toggler"
              data-bs-toggle="collapse"
              href="#brandFilterMenu"
              aria-expanded="true"
              aria-controls="brandFilterMenu"
              >Filtrar por categoria</a
            >
           
            <div class="expand-lg collapse show" id="brandFilterMenu">
              <h6 class="sidebar-heading d-none d-lg-block">Categorias</h6>
              <form class="mt-4 mt-lg-0" action="#">
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="brand0"
                      type="checkbox"
                      name="clothes-brand"
                      checked
                    />
                    <label class="form-check-label" for="brand0"
                      >Calvin Klein <small>(18)</small></label
                    >
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="brand1"
                      type="checkbox"
                      name="clothes-brand"
                      checked
                    />
                    <label class="form-check-label" for="brand1"
                      >Levi Strauss <small>(30)</small></label
                    >
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="brand2"
                      type="checkbox"
                      name="clothes-brand"
                    />
                    <label class="form-check-label" for="brand2"
                      >Hugo Boss <small>(120)</small></label
                    >
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="brand3"
                      type="checkbox"
                      name="clothes-brand"
                    />
                    <label class="form-check-label" for="brand3"
                      >Tomi Hilfiger <small>(70)</small></label
                    >
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="brand4"
                      type="checkbox"
                      name="clothes-brand"
                    />
                    <label class="form-check-label" for="brand4"
                      >Tom Ford <small>(110)</small></label
                    >
                  </div>
                </div>
              </form>
            </div>
          </div> -->

          <!-- SIZE FILTER -->

          <!--<div class="px-3 sidebar-block px-lg-0 me-lg-4">
            <a
              class="d-lg-none block-toggler"
              data-bs-toggle="collapse"
              href="#sizeFilterMenu"
              aria-expanded="false"
              aria-controls="sizeFilterMenu"
              >Filtrar por talle</a
            >
            
            <div class="expand-lg collapse" id="sizeFilterMenu">
              <h6 class="sidebar-heading d-none d-lg-block">Filtrar por talle</h6>
              <form class="mt-4 mt-lg-0" action="#">
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="size0"
                      type="radio"
                      name="size"
                      v-on:change="filterBySize($event)"
                      value="44"
                    />
                    <label class="form-check-label" for="size0">44</label>
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="size1"
                      type="radio"
                      name="size"
                      v-on:change="filterBySize($event)"
                      value="43"
                    />
                    <label class="form-check-label" for="size1">43</label>
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="size2"
                      type="radio"
                      name="size"
                      v-on:change="filterBySize($event)"
                      value="42"
                    />
                    <label class="form-check-label" for="size2">42</label>
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="size3"
                      type="radio"
                      name="size"
                      v-on:change="filterBySize($event)"
                      value="41"
                    />
                    <label class="form-check-label" for="size3">41</label>
                  </div>
                </div>
                <div class="mb-1">
                  <div class="form-check">
                    <input
                      class="form-check-input"
                      id="size4"
                      type="radio"
                      name="size"
                      
                      value="40"
                      v-on:change="filterBySize($event)"
                    />
                    <label class="form-check-label" for="size3">40</label>
                  </div>
                </div>
              </form>
            </div>
          </div>-->

          <!-- COLOR FILTER -->
          <!-- <div class="px-3 sidebar-block px-lg-0 me-lg-4">
            <a
              class="d-lg-none block-toggler"
              data-bs-toggle="collapse"
              href="#colourFilterMenu"
              aria-expanded="false"
              aria-controls="colourFilterMenu"
              >Filtrar por color</a
            >
          
            <div class="expand-lg collapse" id="colourFilterMenu">
              <h6 class="sidebar-heading d-none d-lg-block">Color</h6>
              <div class="mt-4 mt-lg-0">
                <ul class="mb-0 list-inline colours-wrapper">
                  <li class="list-inline-item">
                    <label
                      class="btn-colour"
                      for="colour_sidebar_Blue"
                      style="background-color: #668cb9"
                      data-allow-multiple
                    >
                    </label>
                    <input
                      class="input-invisible"
                      type="radio"
                      name="colour"
                      value="value_sidebar_Blue"
                      id="colour_sidebar_Blue"
                    />
                  </li>
                  <li class="list-inline-item">
                    <label
                      class="btn-colour"
                      for="colour_sidebar_White"
                      style="background-color: #fff"
                      data-allow-multiple
                    >
                    </label>
                    <input
                      class="input-invisible"
                      type="checkbox"
                      name="colour"
                      value="value_sidebar_White"
                      id="colour_sidebar_White"
                    />
                  </li>
                  <li class="list-inline-item">
                    <label
                      class="btn-colour"
                      for="colour_sidebar_Violet"
                      style="background-color: #8b6ea4"
                      data-allow-multiple
                    >
                    </label>
                    <input
                      class="input-invisible"
                      type="checkbox"
                      name="colour"
                      value="value_sidebar_Violet"
                      id="colour_sidebar_Violet"
                    />
                  </li>
                  <li class="list-inline-item">
                    <label
                      class="btn-colour"
                      for="colour_sidebar_Red"
                      style="background-color: #dd6265"
                      data-allow-multiple
                    >
                    </label>
                    <input
                      class="input-invisible"
                      type="checkbox"
                      name="colour"
                      value="value_sidebar_Red"
                      id="colour_sidebar_Red"
                    />
                  </li>
                </ul>
              </div>
            </div>
          </div> -->
        </div>
        <!-- /Sidebar end-->
      </div>
    </div>
  </div>
</template>

<style>
.product-image {
  border-bottom: 1px solid #474747 !important;
}

.breadcrumb {
  padding: 1rem 0 !important;
}

.block-toggler[data-bs-toggle="collapse"]::before {
  display: none;
}

.page-item.active .page-link {
  background-color: #1c4c3b !important;
  color: white !important;
}
</style>

<script>
import noUiSlider from "../../../public/assets/js/nouislider.min.mjs";
import currencyFormatter from "currency-formatter";
import axios from "axios";

export default {
  data() {
    return {
      slider: {
        startMin: 1000,
        startMax: 10000,
        min: 0,
        max: 10000,
        start: 1000,
        step: 1,
      },
      minRange: null,
      maxRange: null,
      allProducts: [],
      products: [],
      currentPage: 1,
      perPage: 12,
      sortBy: "Por defecto",
      get itemsForList() {
        return this.allProducts.slice(
          (this.currentPage - 1) * this.perPage,
          this.currentPage * this.perPage
        );
      },
      categories: [],
      activeCat: "",
      activeSubcat: "",
      loading: true,
      fullPage: true,
      USDData: {},
      USDEnabled: null,
    };
  },
  mounted() {
    noUiSlider.create(this.$refs.priceSlider, {
      start: [this.slider.startMin, this.slider.startMax],
      step: this.slider.step,
      range: {
        min: [this.slider.min],
        max: [this.slider.max],
      },
    });
    this.$refs.priceSlider.noUiSlider.on("update", (values, handle) => {
      this[handle ? "maxRange" : "minRange"] = parseInt(values[handle]);
    });
    window.scrollTo(0, 0);
  },
  beforeMount() {
    var loader = this.$loading.show({
      container: this.fullPage ? null : this.$refs.formContainer,
      canCancel: false,
      color: "#1c4c3b",
      opacity: 1,
    });

    this.getUSDSettings();

    axios
      .get(this.$url + "/public/getAllProducts", {
        headers: {
          "Content-Type": "application/json",
        },
      })
      .then((response) => {
        const { data } = response;
        this.allProducts = data;
        this.products = data;
        this.loading = false;
        //if (this.$route.query.subcategory) {
        //  this.getSubcategoryProducts();
        //}
        //if (this.$route.query.category) {
        //  this.getCategoryProducts();
        //}
        //if (this.$route.query.filter) {
        //  this.filterBySearch();
        //}
        loader.hide();
      })
      .catch((error) => {
        console.log(error.response.data.msg);
        this.msm_error = error.response.data.msg;
        loader.hide();
      });
    this.getCategories();
  },

  methods: {
    scrollToTop() {
      window.scrollTo(0, 0);
    },
    priceConverter(price) {
      return currencyFormatter.format(price, { code: "ARS" });
    },
    showPerPage(n) {
      this.perPage = n;
    },
    setSortBy() {
      if (this.sortBy == "Por defecto") {
        this.allProducts.sort((a, b) =>
          new Date(a.createdAt).getTime() < new Date(b.createdAt).getTime()
            ? 1
            : -1
        );
      }
      if (this.sortBy == "Mayor a menor precio") {
        this.allProducts.sort((a, b) => (a.price < b.price ? 1 : -1));
      }
      if (this.sortBy == "Menor a mayor precio") {
        this.allProducts.sort((a, b) => (a.price > b.price ? 1 : -1));
      }
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
          if (this.$route.query.subcategory && this.$route.query.category) {
            const categoryActive = this.categories.filter((item) =>
              item.subcategories.some(
                (subcat) =>
                  subcat.name == this.$route.query.subcategory &&
                  subcat.categoryName == this.$route.query.category
              )
            );
            this.activeCat = categoryActive[0].category._id;
            this.activeSubcat = this.$route.query.subcategory;
          }

          if (this.$route.query.category) {
            const categoryActive = this.categories.filter(
              (item) => item.category.name == this.$route.query.category
            );
            this.activeCat = categoryActive[0].category._id;
          }
        })
        .catch((error) => {
          console.log(error.response.data.msg);
          this.msm_error = error.response.data.msg;
        });
    },
    redirectToSubcategory(subcat, cat) {
      this.activeCat = cat.category._id;
      this.activeSubcat = subcat.name;
      this.$router.push({
        name: "products",
        query: { category: cat.category.name, subcategory: subcat.name },
      });
      this.getSubcategoryProducts();
    },
    getSubcategoryProducts() {
      this.allProducts = this.products.filter(
        (item) =>
          item.subcategory == this.$route.query.subcategory &&
          item.category == this.$route.query.category
      );
    },
    redirectToCategory(category) {
      this.activeCat = category._id;
      this.$router.push({
        path: "/products",
        query: { category: category.name },
      });
      this.getCategoryProducts();
    },
    getCategoryProducts() {
      this.allProducts = this.products.filter(
        (item) => item.category == this.$route.query.category
      );
    },
    filterBySize(e) {
      this.allProducts = this.products.filter((products) =>
        products.variants.some((variant) => variant.variant == e.target.value)
      );
    },
    filterBySearch() {
      this.allProducts = this.products.filter((product) =>
        product.name
          .toLowerCase()
          .includes(this.$route.query.filter.toLowerCase())
      );
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
  watch: {
    $route(to, from) {
      if (!this.$route.query.subcategory && !this.$route.query.category) {
        this.allProducts = this.products;
      }
      if (this.$route.query.subcategory && this.$route.query.category) {
        this.getSubcategoryProducts();
      }
      if (this.$route.query.filter) {
        this.filterBySearch();
      }
    },
    products(to, from) {
      //console.log("to", to);
      //console.log("from", from);
      //console.log("this.$route.query.subcategory", this.$route.query);
      if (to.length > 0) {
        //console.log("products has length");
        if (!this.$route.query.subcategory && !this.$route.query.category) {
          this.allProducts = this.products;
        }
        if (this.$route.query.subcategory) {
          this.getSubcategoryProducts();
        }
        if (this.$route.query.category && !this.$route.query.subcategory) {
          this.getCategoryProducts();
        }
        if (this.$route.query.filter) {
          this.filterBySearch();
        }
      }
    },
    minRange: function (value) {
      this.allProducts = this.products.filter((item) => item.price >= value);
    },
    maxRange: function (value) {
      this.allProducts = this.products.filter((item) => item.price <= value);
    },
  },
};
</script>

<style>
.hero-heading {
  margin-bottom: 1rem;
}

.product-image {
  height: fit-content !important;
}

.sidebar-menu-item[data-bs-toggle="collapse"]::before {
  display: none !important;
}

.nav-pills .nav-link.active,
.nav-pills .show > .nav-link {
  color: #ffffff !important;
  background-color: black !important;
}

.noUi-horizontal {
  background-color: black !important;
  height: 7px !important;
  padding-bottom: 4px !important;
}

.noUi-horizontal .noUi-handle {
  background: black !important;
  width: 0.4rem !important;
  height: 1.3rem !important;
  border-radius: 10px !important;
}

.page-link {
  color: black !important;
}

.page-item .active {
  color: white !important;
  background-color: #ffffff !important  ;
}

.page-item.active .page-link {
  background-color: #1c4c3b !important;
  color: white !important;
  border: none;
  font-size: 12px;
}

.subcatActive {
  background-color: rgba(207, 207, 207, 0.95) !important;
}
</style>
