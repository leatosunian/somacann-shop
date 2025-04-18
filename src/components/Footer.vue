<template>
  <div>
    <footer class="main-footer" style="background-color: #1c4c3b">
      <!-- Main block - menus, subscribe form-->
      <div
        class="text-muted borde"
        style="background-color: #1c4c3b; padding-top: 2rem"
      >
        <div class="container px-4">
          <div class="row">
            <div class="mb-4 col-lg-5 mb-lg-0">
              <img
                src="/assets/cannabicaLong.png"
                style="width: 300px"
                alt="Cannabica brand logo"
              />
              <!-- <img src="@/assets/new-deco.png" class="logoImg" style="width:47px!important;" alt=""> -->
            </div>

            <div class="mb-4 col-lg-2 col-md-6 mb-lg-0">
              <h6 class="mb-3 text-white text-uppercase">Shop</h6>
              <ul style="margin-bottom: 0px" class="list-unstyled">
                <li>
                  <router-link
                    to="/products?category=STICKERS#!"
                    class="text-white orangeHover"
                    href="#"
                    >Inicio</router-link
                  >
                </li>
                <li>
                  <router-link
                    to="/products"
                    class="text-white orangeHover"
                    href="#"
                    >Todos los productos</router-link
                  >
                </li>
                <li>
                  <router-link
                    to="/products?category=Vaporizadores"
                    class="text-white orangeHover"
                    href="#"
                    >Vaporizadores</router-link
                  >
                </li>
              </ul>
            </div>

            <div class="mb-5 col-lg-2 col-md-6 mb-lg-0">
              <h6 class="mb-3 text-white text-uppercase">Clientes</h6>
              <ul style="margin-bottom: 0px" class="list-unstyled">
                <li>
                  <router-link to="/login" class="text-white orangeHover"
                    >Iniciar sesión</router-link
                  >
                </li>
                <li>
                  <router-link to="/login" class="text-white orangeHover"
                    >Quiero registrarme</router-link
                  >
                </li>
                <li>
                  <span
                    v-b-modal.modal-lg-buy
                    variant="primary"
                    class="orangeHover"
                    style="
                      border: none;
                      margin-top: 0px;
                      margin-left: 0 !important;
                    "
                  >
                    ¿Cómo comprar?
                  </span>
                </li>
                <li>
                  <a
                    class="text-white orangeHover"
                    href="https://api.whatsapp.com/send?phone=5492235892260"
                    target="_blank"
                    >Atención al cliente</a
                  >
                </li>
              </ul>

              <b-modal
                id="modal-lg-buy"
                size="lg"
                title="Cómo comprar"
                style="border-radius: 5px !important"
              >
                <div
                  style="
                    display: flex;
                    flex-direction: column;
                    padding: 0 30px;
                    gap: 10px;
                    border-radius: 5px;
                  "
                >
                  <span style="font-weight: 800; font-size: 18px">
                    Registrate e iniciá sesión
                    <p style="font-weight: 400; font-size: 14px">
                      Para comprar debes ser un usuario registrado. Creá tu
                      cuenta haciendo
                      <router-link to="/login">click acá</router-link> y luego
                      iniciá sesión.
                    </p>
                  </span>
                  <span style="font-weight: 600; font-size: 18px">
                    Agregá un domicilio de entrega
                    <p style="font-weight: 400; font-size: 14px">
                      En las configuraciones de tu cuenta, ingresá hasta dos
                      direcciones de envío para seleccionar al hacer tus
                      compras.
                    </p>
                  </span>
                  <span
                    style="
                      font-weight: 600;
                      font-size: 18px;
                      margin-bottom: 16px;
                    "
                  >
                    Agregá productos a tu carrito
                  </span>
                  <span style="font-weight: 600; font-size: 18px">
                    Realizá el pedido
                    <p style="font-weight: 400; font-size: 14px">
                      Elegí cómo querés que te llegue tu pedido, seleccioná tu
                      dirección de envío que agregaste anteriormente y aboná tu
                      compra de manera segura mediante MercadoPago.
                    </p>
                  </span>
                  <span style="font-weight: 600; font-size: 18px">
                    ¿Cómo sigo mi pedido?
                    <p style="font-weight: 400; font-size: 14px">
                      Cuando despachemos tu pedido, te enviaremos un código de
                      seguimiento para que sigas el estado de tu compra. Éste lo
                      podrás ver ingresando a Mis pedidos, donde en el detalle
                      del pedido se mostrará luego de que te lo enviemos.
                    </p>
                  </span>
                </div>
                <template #modal-footer>
                  <div class=""></div>
                </template>
              </b-modal>
            </div>

            <div class="col-lg-3">
              <h6 class="mb-3 text-white text-uppercase">Contactanos</h6>

              <div style="display: flex; flex-direction: column; gap: 8px">
                <a
                  class="text-muted text-decoration-none"
                  href="https://www.instagram.com/cannabicagrow.shop"
                  target="_blank"
                  title="Instagram"
                >
                  <img
                    src="/assets/instagram.png"
                    alt=""
                    style="width: 19px; margin-right: 10px"
                  />
                  <span class="text-white orangeHover">cannabicagrow.shop</span>
                </a>
                <a
                  class="text-muted text-decoration-none"
                  href="https://api.whatsapp.com/send/?phone=5492236060459&text&type=phone_number&app_absent=0"
                  target="_blank"
                  title="Whatsapp"
                >
                  <img
                    src="/assets/whatsapp.png"
                    alt=""
                    style="width: 20px; margin-right: 8px"
                  />
                  <span class="text-white orangeHover">+54 9 223 606-0459</span>
                </a>
                <div class="flex">
                  <img
                    src="/assets/mail.png"
                    alt=""
                    style="width: 20px; margin-right: 8px"
                  />
                  <span class="text-white orangeHover"
                    >cannabicagroup@gmail.com</span
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div
        style="
          margin: 0 auto;
          width: 90vw;
          height: 1px;
          background-color: #ffffff38;
          margin-top: 2rem;
        "
      ></div>

      <!-- Copyright section of the footer-->
      <div
        class="flex justify-center text-white fw-light"
        style="background-color: #1c4c3b; padding: 1.2rem 15px; font-size: 13px"
      >
        <p class="mb-0 text-center">
          Cannabica Group &copy; Todos los derechos reservados. Tienda
          desarrollada por
          <a
            style="color: white; font-weight: 600"
            target="_blank"
            href="https://tosunian.dev"
            >tosunian.dev</a
          >
        </p>
        <!-- <div class="col-md-6">
                    <ul class="mt-2 mb-0 text-center list-inline mt-md-0 text-md-end">
                      <li class="list-inline-item">
                        <img class="w-2rem" src="https://d19m59y37dris4.cloudfront.net/sell/2-0/img/visa.svg" alt="...">
                      </li>
                      <li class="list-inline-item">
                        <img class="w-2rem" src="https://d19m59y37dris4.cloudfront.net/sell/2-0/img/mastercard.svg" alt="...">
                      </li>
                    </ul>
                  </div> -->
      </div>
    </footer>
  </div>
</template>

<style>
.orangeHover {
  color: white;
  transition: 0.3s all ease-in-out;
}
.orangeHover:hover {
  color: #b8b8b8 !important;
  transition: 0.3s all ease-in-out;
  text-decoration: none;
}
.modal-content {
  border-radius: 8px !important;
}
.close {
  border: 1px solid #04040424;
  border-radius: 4px;
  color: red;
}
</style>

<script>
export default {
  name: "Footer",
};
</script>
