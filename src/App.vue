<template>
  <div id="app">

    <section class="home" v-show="page == 'home'"> <br><br><br>

      <img class="logo" src="https://lh3.googleusercontent.com/proxy/Lz76GvNGhMEq8ngBZAETByagoHiC8upboleTsYcuXzjzkjP_aT-w93BaOPRWXHSp_8_GzAXCua9xTHDp_IMj52y4jE8namQJnwAKeUEeZZmo7WGZSpQSLPXgVA"> <br><br>

      <label>
        <img class="qr" src="https://static.thenounproject.com/png/78107-200.png"> <br><br>

        <p>Toca la pantalla para</p>
        <p><b>Capturar QR</b></p>

        <input type=file accept="image/*" capture=environment @change="openQRCamera" tabindex=-1 style="display: none;">
      </label>

    </section>

    <section class="details" v-show="page == 'details'">
      <header>
        <img class="logo" src="https://lh3.googleusercontent.com/proxy/Lz76GvNGhMEq8ngBZAETByagoHiC8upboleTsYcuXzjzkjP_aT-w93BaOPRWXHSp_8_GzAXCua9xTHDp_IMj52y4jE8namQJnwAKeUEeZZmo7WGZSpQSLPXgVA">
      </header>
      <section>
        <p>SKU: 7707304621360</p>
        <p>Descripción: Plus AA x 12 unid</p>
        <p>Embalaje: Caja x 12</p>
        <p>Pallet: 12 cajas (1728 unid)</p> <br>

        <img src="https://es.qr-code-generator.com/wp-content/themes/qr/new_structure/markets/core_market/generator/dist/generator/assets/images/websiteQRCode_noFrame.png"> <br>

        <button>Ingresar en inventario</button>
      </section>
    </section>

  </div>
</template>

<script>

export default {
  name: 'App',
  data: () => {
    return {
      page: 'home',
      // page: 'details',
      value: '',
    }
  },
  mounted: () => {
    // console.log('scan ...')
  },
  methods: {
    openQRCamera: function (event) {
      let node = event.target
      let self = this
      var reader = new FileReader()
      reader.onload = function() {
        qrcode.callback = function(res) {
          if(res instanceof Error) {
            // alert("Asegúrese de que el código QR esté dentro del marco de la cámara e intente nuevamente.")

            self.value = res
            self.page = 'details'

          } else {
            // console.log('res: ', res)
            self.value = res
            self.page = 'details'
          }
        };
        qrcode.decode(reader.result)
      };
      reader.readAsDataURL(node.files[0])
    }
  }
}
</script>

<style lang="stylus">
  /* reset */
  body
  p
    margin 0
  button
    outline 0
    border 0

  /* general */
  body
    font-family 'Arial'

  /* home */
  .home
    background #30da7b
    height 100vh
    .logo
      max-width 150px
      margin auto
      display table
    .qr
      margin auto
      display table
    p
      text-align center
      color #eee
      font-size 20px
      b
        color #fff

  /* details */
  .details
    header
      background #30da7b
      padding 8px 16px
      img
        width 100px
    section
      padding 16px
      p
        margin 8px 0
      img
        max-width 240px
        margin auto
        display table
      button
        background #30da7b
        border-radius 4px
        font-family 'Arial'
        color white
        font-size 16px
        padding 12px 16px
        display table
        margin auto

</style>
