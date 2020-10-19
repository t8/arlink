<template>
  <div id="app">
    <div class="hero is-fullheight is-light">
      <div class="hero-body">
        <div class="container">
          <div class="box">
            <h1 class="title is-2 has-text-centered"><span class="has-text-500">Ar</span><span class="has-text-700">Link</span></h1>
            <div class="columns">
              <div class="column">
                <input class="input is-medium" type="text" placeholder="Address">
              </div>
              <div class="column">
                <div class="select is-medium is-fullwidth">
                  <select>
                    <option>ETH</option>
                  </select>
                </div>
              </div>
            </div>
            <button class="button is-large is-fullwidth"><span class="has-text-rainbow has-text-700">Link</span></button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {

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

      button {
        -webkit-transition: background-color 100ms linear;
        -ms-transition: background-color 100ms linear;
        transition: background-color 100ms linear;
        margin-top: 40px;
        border: none;
        border-radius: 24px;
        background: #ffffff;
        box-shadow: 5px 5px 14px #e8e8e8, 
                    -5px -5px 14px #ffffff;

        &:hover {
          -webkit-transition: background-color 100ms linear;
          -ms-transition: background-color 100ms linear;
          transition: background-color 100ms linear;
          background: #fcfcfc;
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
