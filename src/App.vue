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

      <div class="hero-body" v-if="footer_index == 1 | footer_index == 2">
        <div class="container">
          <div id= "Encrypt info" v-if="footer_index == 1">
            <p class="title">
              Encrypt a message using an image for the key
            </p>
            <p class="subtitle is-5">
              Placeholder description goes here.
            </p>
          </div>

          <div id= "Decrypt info" v-if="footer_index == 2">
            <p class="title">
              Decrypt a message using an image for the key
            </p>
            <p class="subtitle is-5">
              Placeholder description goes here.
            </p>
          </div>
          
          <br>
          <br>
          <div class="columns">
            <div class="column ">
              <textarea class="textarea is-link has-fixed-size" placeholder="Enter some text here" rows="14" v-model="left_window_text"></textarea>
              <br>
              <div class = "columns">
                <div class = "column is-three-quarters">
                  <div class="file is-medium has-name is-info" >
                    <label class="file-label">
                      <input class="file-input" type="file" accept="image/*" @change="file_check">
                      <span class="file-cta">
                        <span class="file-icon">
                          <i class="fa fa-file-image-o"></i>
                        </span>
                        <span class="file-label">
                          Image Key
                        </span>
                      </span>
                      <span class="file-name">
                        {{image_name}}
                      </span>
                    </label>
                  </div>
                  <div class = "subtitle has-text-danger" v-if="error_log != ''">
                    {{error_log}}
                  </div>
                  <br v-else>
                </div>
                <div class = "column">
                  <button class="button is-light" @click="encrypt()" v-if="footer_index == 1">
                    <span class="file-icon">
                      <i class="fa fa-code"></i>
                    </span>
                    Encrypt Text
                  </button>
                  <button class="button is-light" @click="decrypt()" v-if="footer_index == 2">
                    <span class="file-icon">
                      <i class="fa fa-code"></i>
                    </span>
                    Decrypt Text
                  </button>
                </div>
              </div>
            </div>
            <div class="column">
              <textarea id = "right_text" class="textarea is-link has-fixed-size" placeholder="Output will show here" rows="14" v-model="right_window_text" readonly></textarea>
              <br>
              <div class = "buttons">
                <button class="button is-dark" @click="copy_text()">
                  <span class="file-icon">
                    <i class="fa fa-clipboard"></i>
                  </span>
                  Copy to Clipboard
                </button>
                <button class="button is-dark" @click="download_text()">
                  <span class="file-icon">
                    <i class="fa fa-download"></i>
                  </span>
                  Download
                </button>
              </div>
            </div>
          </div>
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
      left_window_text: "",
      right_window_text: "",
      suported_files: 
        {
          "jpe":1, "jpg":1, "jpeg":1, "gif":1, "png":1, "bmp":1, 
          "ico":1,"svg":1, "svgz":1, "tif":1, "tiff":1, "ai":1, 
          "drw":1, "pct":1, "psp":1,"xcf":1, "psd":1, "raw":1, 
          "webp":1
        },
      image_name: "No Image Selected",
      image_file: undefined,
      error_log: "",
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
      app.data.footer_1 = "has-text-white";
      app.data.footer_2 = "has-text-white";
      app.data.footer_3 = "has-text-white";
      app.data.footer_4 = "has-text-white";
      
      if (app.data.footer_index != index)
      {
        app.data.image_name = "No Image Selected";
        app.data.image_file = undefined;
        app.data.left_window_text = "";
        app.data.right_window_text = "";
        app.data.error_log = "";
      }

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
    },

    file_check: function(event)
    {
      let file = event.target.files[0];
      app.data.image_name = file.name;
      let name_parts = file.name.split(".");

      if (name_parts.length < 2)
      {
        app.data.error_log = "Not a valid image";
        app.data.image_name = file.name;
      }
      else
      {
        let type = name_parts[name_parts.length-1];
        if (type in app.data.suported_files)
        {
          app.data.image_file = file;
          app.data.error_log = "";
        }
        else
        {
          app.data.error_log = "Not a valid image";
          app.data.image_name = file.name;
        }
      }
    },

    encrypt: function()
    {
      let crypto = require('crypto')
      let reader = new FileReader();

      if(app.data.left_window_text == "")
      {
        app.data.error_log = "Input text to encrypt";
        return;
      }
      else if(app.data.image_file == undefined)
      {
        app.data.error_log = "Missing an image for encryption";
        return;
      }
      else
      {
        app.data.error_log = "";
      }

      reader.addEventListener("load", function()
      {
        let long_key = reader.result;
        let crypto_key = crypto.createCipher("aes-128-cbc", long_key);
        let result = crypto_key.update(app.data.left_window_text, "utf-8", "hex");
        result += crypto_key.final("hex");
        app.data.right_window_text = result;

      }, false);
      reader.readAsDataURL(app.data.image_file);
    },

    decrypt: function()
    {
      let crypto = require('crypto')
      let reader = new FileReader();

      if(app.data.left_window_text == "")
      {
        app.data.error_log = "Input text to decrypt";
        return;
      }
      else if(app.data.image_file == undefined)
      {
        app.data.error_log = "Missing an image for decryption";
        return;
      }
      else
      {
        app.data.error_log = "";
      }

      reader.addEventListener("load", function()
      {
        let long_key = reader.result;
        let crypto_key = crypto.createDecipher("aes-128-cbc", long_key);
        let result = crypto_key.update(app.data.left_window_text, "hex", "utf8");
        result += crypto_key.final("utf8");
        app.data.right_window_text = result;

      }, false);
      reader.readAsDataURL(app.data.image_file);
    },

    copy_text: function()
    {
      let right_text = document.getElementById("right_text");
      right_text.select();
      document.execCommand("copy");
    },

    download_text: function()
    {
      let element = document.createElement("a");
      element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(app.data.right_window_text));
      element.setAttribute('download', "message.txt");
      document.body.appendChild(element);
      element.click();
      document.body.removeChild(element);
    },
  };

  module.exports = {
    name: "index",
    data: function () {
      return app.data;
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