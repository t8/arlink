<template>
  <div id="app">
    <div class="hero is-fullheight is-light">
      <div class="hero-body">
        <div class="container">
          <div class="box">
            <h1 class="title is-2 has-text-centered"><span class="has-text-500">Ar</span><span class="has-text-700">Link</span></h1>
            <div class="columns">
              <div class="column">
                <input class="input is-medium" type="text" placeholder="Address" v-model="address">
              </div>
              <div class="column">
                <div class="select is-medium is-fullwidth">
                  <select v-model="currency">
                    <option selected>ETH</option>
                    <option>BTC</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="columns">
              <div class="column">
                <div class="file is-medium is-fullwidth">
                  <label class="extruded file-label">
                    <input class="file-input" type="file" name="keyfile" accept="application/json" @change="onFileChange">
                    <span class="file-cta">
                      <span class="file-icon">
                        <font-awesome-icon :icon="['fas', 'key']" />
                      </span>
                      <span class="file-label">
                        Attach your keyfile
                      </span>
                    </span>
                  </label>
                </div>
              </div>
              <div class="column">
                <button class="button extruded is-medium is-fullwidth" @click="commenceUpload" :disabled="success">
                  <span v-if="!success" class="has-text-rainbow has-text-700">Link</span>
                  <font-awesome-icon v-if="success" :icon="['fas', 'check']" />
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Arweave from 'arweave';

export default {
  name: 'App',
  data() { 
    return {
      keyfile: {},
      address: "",
      currency: "ETH",
      success: false
    }
  },
  methods: {
    // Thanks to: raymondcamden.com/2019/05/21/reading-client-side-files-for-validation-with-vuejs
    onFileChange(event) {
      let file = event.target.files[0];
      const reader = new FileReader();
      reader.readAsText(file, "UTF-8");
      reader.onload =  evt => {
        this.keyfile = JSON.parse(evt.target.result);
      }
      reader.onerror = evt => {
        console.error(evt);
      }
    },
    async commenceUpload() {
      const arweave = Arweave.init({
        host: 'arweave.net',
        port: 443,
        protocol: 'https',
        timeout: 20000,
        logging: false,
      });

      // Create the tx
      let transaction = await arweave.createTransaction({
        data: Math.random().toString().slice(-4)
      }, this.keyfile);

      // Add the necessary tags
      transaction.addTag("Application", "ArLink");
      transaction.addTag("Chain", this.currency);
      transaction.addTag("Wallet", this.address);

      await arweave.transactions.sign(transaction, this.keyfile);
      try {
        // Post the tx

        const response = await arweave.transactions.post(transaction);
        if (response.status === 200) {
          // It succeeded
          this.success = true;
        } else {
          console.error("Something went wrong with posting the transaction");
        }
      } catch (error) {
        console.error(error);
      }
    }
  }
}
</script>

<style lang="scss">
  @import url('https://rsms.me/inter/inter.css');

  @supports (font-variation-settings: normal) {
    html { 
      font-family: 'Inter var', sans-serif; 
    }
  }

  @font-face{
    font-family: 'JetBrainsMono';
    src: url('https://cdn.jsdelivr.net/gh/JetBrains/JetBrainsMono/web/woff2/JetBrainsMono-Regular.woff2') format('woff2'),
      url('https://cdn.jsdelivr.net/gh/JetBrains/JetBrainsMono/web/woff/JetBrainsMono-Regular.woff') format('woff'),
      url('https://cdn.jsdelivr.net/gh/JetBrains/JetBrainsMono/ttf/JetBrainsMono-Regular.ttf') format('truetype');
    font-weight: 400;
    font-style: normal;
  }

  #app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    .title {
      font-family: 'Inter', sans-serif;
    }

    p {
      font-family: 'JetBrainsMono', serif;
    }

    .box {
      border-radius: 24px;
      background: #ffffff;
      box-shadow:  5px 5px 10px #ebebeb, 
                  -5px -5px 10px #ffffff;
      width: 50%;
      margin: 20px auto;
      min-width: 300px;
      max-width: 600px;

      .input, select {
        border: none;
        border-radius: 24px;
        background: #ffffff;
        box-shadow: inset 2px 2px 10px #ebebeb, 
                    inset -2px -2px 10px #ffffff;    
      }

      .extruded {
        -webkit-transition: all 100ms linear;
        -ms-transition: all 100ms linear;
        transition: all 100ms linear;
        margin-top: 40px;
        border: none;
        border-radius: 24px;
        background: #ffffff;

        &.button {
          &:hover {
            -webkit-transition: all 100ms linear;
            -ms-transition: all 100ms linear;
            transition: all 100ms linear;
            box-shadow: 5px 5px 14px #e8e8e8, 
                        -5px -5px 14px #ffffff;
          }
        }

        .file-cta {
          border: none;
          background-color: white;
        }
      }
    }

    .has-text-500 {
      font-weight: 500;
    }

    .has-text-700 {
      font-weight: 700;
    }

    .has-text-rainbow {
      background: linear-gradient( 92deg, #95d7e3, #eb76ff );
      background: -webkit-linear-gradient( 92deg, #95d7e3, #eb76ff );
      background-size:600vw 600vw;
      
      background-clip: text;
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      animation: textAnimate 5s linear infinite alternate;
    }

    @keyframes textAnimate {
      from {
        filter: hue-rotate(0deg);
        background-position-x: 0%;
        
      }
      to {
        filter: hue-rotate(360deg);
        background-position-x: 600vw;
      }
    }
  }
</style>
