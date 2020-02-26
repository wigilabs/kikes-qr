<template>
  <div id="app">

    <section class="home"> <br><br><br>

      <img class="logo" src="https://lh3.googleusercontent.com/proxy/Lz76GvNGhMEq8ngBZAETByagoHiC8upboleTsYcuXzjzkjP_aT-w93BaOPRWXHSp_8_GzAXCua9xTHDp_IMj52y4jE8namQJnwAKeUEeZZmo7WGZSpQSLPXgVA"> <br><br>

      <label>
        <img class="qr" src="https://static.thenounproject.com/png/78107-200.png"> <br><br>

        <p>Toca la pantalla para</p>
        <p><b>Capturar QR</b></p>

        <input type=file accept="image/*" capture=environment @change="openQRCamera" tabindex=-1 style="display: none;">
      </label>

    </section>

  </div>
</template>

<script>

// QR
// window.openQRCamera = function (node, type) {
//   var reader = new FileReader();
//   reader.onload = function() {
//     node.value = "";
//     qrcode.callback = function(res) {
//       if(res instanceof Error) {
//         alert("Asegúrese de que el código QR esté dentro del marco de la cámara e intente nuevamente.");
//       } else {
//         console.log('res: ', res)
//       }
//     };
//     qrcode.decode(reader.result);
//   };
//   reader.readAsDataURL(node.files[0]);
// }

// window.showQRIntro = function () {
//   return confirm("Tomar una foto al QR del cliente.");
// }

export default {
  name: 'App',
  data: () => {
    return {
      text: 'Vue.js'
    }
  },
  mounted: () => {
    console.log('scan ...')
  },
  methods: {
    openQRCamera: function (event) {
      let node = event.target
      console.log('node: ', node)

      let self = this

      var reader = new FileReader();
      reader.onload = function() {
        node.value = "";
        qrcode.callback = function(res) {
          if(res instanceof Error) {
            alert("Asegúrese de que el código QR esté dentro del marco de la cámara e intente nuevamente.");
          } else {
            console.log('res: ', res)
            self.text = res
          }
        };
        qrcode.decode(reader.result);
      };
      reader.readAsDataURL(node.files[0]);
    }
  }
}
</script>

<style lang="stylus">
  /* reset */
  body
  p
    margin 0

  /* code */
  body
    background #30da7b
    font-family 'Arial'

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

</style>
