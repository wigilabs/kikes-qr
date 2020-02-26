<template>
  <div id="app">
    Hello! {{ text }}

    <br>

    <label>
      <input type=file accept="image/*" capture=environment onchange="openQRCamera(this, 'send');" tabindex=-1>
    </label>

  </div>
</template>

<script>

// QR
window.openQRCamera = function (node, type) {
  var reader = new FileReader();
  reader.onload = function() {
    node.value = "";
    qrcode.callback = function(res) {
      if(res instanceof Error) {
        alert("Asegúrese de que el código QR esté dentro del marco de la cámara e intente nuevamente.");
      } else {
        console.log('res: ', res)
      }
    };
    qrcode.decode(reader.result);
  };
  reader.readAsDataURL(node.files[0]);
}

window.showQRIntro = function () {
  return confirm("Tomar una foto al QR del cliente.");
}

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
    scan: function () {
      console.log('scan ...')
    }
  }
}
</script>

<style lang="stylus">
  /* reset */
  body
    margin 0

  /*video
    height 100vh
    width 100vw*/

</style>
