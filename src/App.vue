<template>
  <div>
    <section class="hero gradient-area-primary is-fullheight">
      <div class="hero-head">
        <header class="navbar">
          <div class="container">
            <div class="navbar-brand">
              <a class="navbar-item title is-1 has-text-dark is-family-code" href="/messcrypt/">
                Messcrypt
              </a>
              <span class="navbar-burger" data-target="navbarMenuHeroC">
                <span></span>
                <span></span>
                <span></span>
              </span>
            </div>
            <div id="navbarMenuHeroC" class="navbar-menu">
              <div class="navbar-end">
                <a class="navbar-item" :class="navbar_features" v-on:click="nav_select(0)">
                  Features
                </a>
                <a class="navbar-item" :class="navbar_about" v-on:click="nav_select(1)">
                  About
                </a>
                <a class="navbar-item" :class="navbar_contact" v-on:click="nav_select(2)">
                  Contact
                </a>
                <span class="navbar-item">
                  <a class="button is-inverted" href="https://github.com/MarlonGregorio/messcrypt">
                    <span class="icon">
                      <i class="fa fa-github"></i>
                    </span>
                    <span>Repository</span>
                  </a>
                </span>
              </div>
            </div>
          </div>
        </header>
      </div>

      <div class="hero-body" v-if="footer_index == 1">
        <div class="container">
          <p class="title">
            Encrypt a message using an image for the key
          </p>
          <p class="subtitle is-5">
            Placeholder description goes here.
          </p>
          <br>
          <div class="columns">
            <div class="column ">
              <textarea class="textarea is-link has-fixed-size" placeholder="Enter some text here" rows="14"></textarea>
              <br>
              <div class="file is-medium has-name is-info">
                <label class="file-label">
                  <input class="file-input" type="file">
                  <span class="file-cta">
                    <span class="file-icon">
                      <i class="fa fa-upload"></i>
                    </span>
                    <span class="file-label">
                      Image key
                    </span>
                  </span>
                  <span class="file-name">
                    No image selected
                  </span>
                </label>
              </div>
            </div>
            <div class="column">
              <textarea class="textarea is-link has-fixed-size" placeholder="Output will show here" rows="14" readonly></textarea>
              <br>
              <button class="button is-dark">
                <span class="file-icon">
                  <i class="fa fa-download"></i>
                </span>
                Download text
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="hero-body" v-if="footer_index == 2">
        <div class="container has-text-centered">
          <p class="title">
            Not yet ready to be shown
          </p>
        </div>
      </div>
      <div class="hero-body" v-if="footer_index == 3">
        <div class="container has-text-centered">
          <p class="title">
            Not yet ready to be shown
          </p>
        </div>
      </div>
      <div class="hero-body" v-if="footer_index == 4">
       <div class="container has-text-centered">
          <p class="title">
            Not yet ready to be shown
          </p>
        </div>
      </div>
      <div class="hero-foot">
        <nav class="tabs is-boxed is-fullwidth">
          <div class="container">
            <ul>
              <li :class="footer_1" v-on:click="footer_select(1)"><a>Encrypt</a></li>
              <li :class="footer_2" v-on:click="footer_select(2)"><a>Decrypt</a></li>
              <li :class="footer_3" v-on:click="footer_select(3)"><a>Tutorial</a></li>
              <li :class="footer_4" v-on:click="footer_select(4)"><a>Examples</a></li>
            </ul>
          </div>
        </nav>
      </div>
    </section>
  </div>
</template>

<script>
  let app = {};

  app.data = {
      navbar_features: "",
      navbar_about: "",
      navbar_contact: "",
      footer_index: 1,
      footer_1: "has-text-primary is-active",
      footer_2: "has-text-white",
      footer_3: "has-text-white",
      footer_4: "has-text-white",
  };

  app.methods = {

    nav_select: function(index) 
    {
      app.data.navbar_features = "";
      app.data.navbar_about = "";
      app.data.navbar_contact = "";

      switch (index)
      {
        case 0:
          app.data.navbar_features = "is-active";
          break;
        case 1:
          app.data.navbar_about = "is-active";
          break;
        case 2:
          app.data.navbar_contact = "is-active";
      }
    },

    footer_select: function(index) 
    {
      app.data.footer_1 = "has-text-white"
      app.data.footer_2 = "has-text-white";
      app.data.footer_3 = "has-text-white";
      app.data.footer_4 = "has-text-white";
      app.data.footer_index = index;

      switch (index)
      {
        case 1:
          app.data.footer_1 = "has-text-primary is-active";
          break;
        case 2:
          app.data.footer_2 = "has-text-primary is-active";
          break;
        case 3:
          app.data.footer_3 = "has-text-primary is-active";
          break;
        case 4:
          app.data.footer_4 = "has-text-primary is-active";
          break;
      }
    }
  };

  module.exports = {
    name: "index",
    data: function () {
      return app.data
    },
    methods: app.methods,
  }
</script>

<style>
  .gradient-area-primary{
    background-color: #abe9cd;
    background-image: linear-gradient(315deg, #3eadcf  0%, #abe9cd 74%);
    min-width: 100%;
    min-height: 100%;
  }
</style>