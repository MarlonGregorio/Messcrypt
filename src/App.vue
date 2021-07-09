<template>
  <div>
    <section class="hero gradient-area-primary is-fullheight">
      <div class="hero-head">
        <header class="navbar">
          <div class="container">
            <div class="navbar-brand">
              <a class="navbar-item title is-1 has-text-dark is-family-code" href="/Messcrypt/">
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
                <a class="navbar-item" :class="navbar_1" v-on:click="nav_select(1)">
                  Home
                </a>
                <a class="navbar-item" :class="navbar_2" v-on:click="nav_select(2)">
                  Features
                </a>
                <a class="navbar-item" :class="navbar_3" v-on:click="nav_select(3)">
                  Contact
                </a>
                <span class="navbar-item">
                  <a class="button is-inverted" href="https://github.com/MarlonGregorio/Messcrypt">
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
              Encrypt a message using an image
            </p>
            <p class="subtitle is-5">
              All main image formats are supported. Encryption is done using AES 128 through the Node.js Crypto module.
            </p>
          </div>
          <div id= "Decrypt info" v-if="footer_index == 2">
            <p class="title">
              Decrypt a message using an image
            </p>
            <p class="subtitle is-5">
              The image key must be the same one that encypted the message. The Metadata is ignored.
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
        <div class="container">
          <p class="title">
            Some examples of encrypted messages using images
          </p>
          <div class = "columns has-text-centered">
            <div class = "column">
              <div class="card">
                <div class="card-image">
                  <figure class="image is-4by3">
                    <img src="https://i.imgur.com/ptebmwD.jpg">
                  </figure>
                </div>
                <div class="card-content">
                  <div class="content">
                    <p class = "title is-4">
                      Cool looking guinea pig
                    </p>
                    <p class = "subtitle">
                      4b5a0a59da2aea578e3749893740e94b591b28be40683eb11f1e10f8ad414a51
                    </p>
                  </div>
                </div>
              </div>
            </div>
            <div class = "column">
              <div class="card">
                <div class="card-image">
                  <figure class="image is-4by3">
                    <img src="https://i.imgur.com/yszIZ8d.jpg">
                  </figure>
                </div>
                <div class="card-content">
                  <div class="content">
                    <p class = "title is-4">
                      Happy looking chihuahua
                    </p>
                    <p class = "subtitle">
                      eb8a0f3f9c865c293f24b26fbe7b57151d05cf8f18987ed1541a92f8f23a570b
                    </p>
                  </div>
                </div>
              </div>
            </div>
            <div class = "column">
              <div class="card">
                <div class="card-image">
                  <figure class="image is-4by3">
                    <img src="https://i.imgur.com/PSOyQJF.jpg">
                  </figure>
                </div>
                <div class="card-content">
                  <div class="content">
                    <p class = "title is-4">
                      Curious looking cat
                    </p>
                    <p class = "subtitle">
                      0d0a449329acaa70ce6c0fbd38b7a00f9dff0ae8a3833fc4aa9ee9d20fa2ab75
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <br>
          <a href="https://www.freepik.com/photos">Photos created by freepik - www.freepik.com</a>
        </div>
      </div>
      <div class="hero-body" v-if="footer_index == 4">
        <div class="container">
          <div class="content">
            <div class = "title">
              Having Issues?
            </div>
            <div class = "subtitle">
              Here are some potential solutions.
            </div>
            <h3>The same message is encrypting differently</h3>
            <ol>
              <li>Check if your message has the same letter case each time. Even a single letter being uppercase can result in a new encryption.</li>
              <li>Check if the image is the same. It has to be an exact copy beside its metadata.</li>
              <li>Make sure you clicked the encrypt button. The oldest encryption is alway shown.</li>
            </ol>
            <h3>Decryption is not working</h3>
            <p>
              Decryption will only work with text in hex format because a hex format string is the result of encryption. 
              Also for the image key to decrypt properly, it has to be exactly the same image used for encryption. 
              The name of the file and other metadata will not affect decryption. 
            </p>
            <h3>Forgot/Lost the image key</h3>
            <p>
              There is no limit to the number of times you can try to decrypt. 
              Try all the images you think might work.
              If you lost the image and cant recreate it in an exact pixel format, there is not much that can be done.
            </p>
            <h3>Issues with nested encryption</h3>
            <p>
              Nested encryption is when you encrypt a message that has already been encrypted. 
              If done multiple times it can get confusing if different image keys are used. 
              Also maybe just avoid using nested encryption as a single encryption should be secure enough.
            </p>
          </div>
        </div>
      </div>
      <div class="hero-body" v-if="navbar_index == 2">
        <div class="container">
           <div class = "content">
            <div class = "title">
              Features about this project
            </div>
            <div class = "subtitle">
              Find out what is being used.
            </div>
            <h3>Hosted on github pages</h3>
            <p>
              The repository is located at <a href = "https://github.com/MarlonGregorio/Messcrypt">github.com/MarlonGregorio/Messcrypt</a>.
            </p>
            <h3>Vue JS</h3>
            <p>
              "Vue (pronounced /vjuː/, like view) is a progressive framework for building user interfaces. 
              Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. 
              The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. 
              On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with
              modern tooling and supporting libraries." -Vue.js documentation
              <br>
              <a href = "https://py4web.com/_documentation/static/index.html ">https://py4web.com</a>
            </p>
            <h3>Crypto</h3>
            <p>
              "The crypto module provides cryptographic functionality that includes a set of wrappers for OpenSSL's hash, HMAC, cipher, decipher, 
              sign, and verify functions." -Crypto documentation
              <br>
              <a href = "https://nodejs.org/api/crypto.html#crypto_crypto">https://nodejs.org/api/crypto.html#crypto_crypto</a>
            </p>
            <h3>Bulma CSS</h3>
            <p>
              "Bulma is a free, open-source CSS framework based on Flexbox and used by more than 200,000 developers. 
              Bulma is also considered a mobile-first framework and optimizes for vertical reading. 
              In the end, Bulma is simply a collection of CSS classes. Write the HTML code you want." -Bulma documentation
              <br>
              <a href = "https://bulma.io ">https://bulma.io </a>
            </p>
            <h3>Font Awesome</h3>
            <p>
              "Font Awesome gives you scalable vector icons that can instantly be customized — size, color, drop shadow, 
              and anything that can be done with the power of CSS." -Font Awesome documentation 
              <br>
              <a href = "https://fontawesome.com/v4.7.0 ">https://fontawesome.com/v4.7.0 </a>
            </p>
           </div>
         </div>
       </div>
       <div class="hero-body" v-if="navbar_index == 3">
        <div class="container">
          <div class = "content">
            <div class = "title">Questions or concerns?</div>
            <div class = "subtitle">
              Contact me through email.
            </div>
            <br>
            <div class = "title is-4">
              Email
            </div>
            <div class = "subtitle is-6">
              marlongregorio1213@gmail.com
            </div>
           </div>
         </div>
       </div>
      <div class="hero-foot" v-if = "navbar_index == 1">
        <nav class="tabs is-boxed is-fullwidth">
          <div class="container">
            <ul>
              <li :class="footer_1" v-on:click="footer_select(1)"><a>Encrypt</a></li>
              <li :class="footer_2" v-on:click="footer_select(2)"><a>Decrypt</a></li>
              <li :class="footer_3" v-on:click="footer_select(3)"><a>Examples</a></li>
              <li :class="footer_4" v-on:click="footer_select(4)"><a>Help</a></li>
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
      navbar_1: "is-active",
      navbar_2: "",
      navbar_3: "",
      navbar_index: 1,
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
      app.data.navbar_1 = "";
      app.data.navbar_2 = "";
      app.data.navbar_3 = "";
      app.data.navbar_index = index;
      switch (index)
      {
        case 1:
          app.data.navbar_1 = "is-active";
          app.methods.footer_select(1);
          break;
        case 2:
          app.data.navbar_2 = "is-active";
          app.data.footer_index = -1;
          break;
        case 3:
          app.data.footer_index = -1;
          app.data.navbar_3 = "is-active";
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
        app.data.error_log = "Invalid image key";
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
          app.data.error_log = "Invalid image key";
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
        app.data.error_log = "Missing text for encryption";
        return;
      }
      else if(app.data.image_file == undefined)
      {
        app.data.error_log = "Missing image key for encryption";
        return;
      }
      else
      {
        app.data.error_log = "";
      }

      reader.addEventListener("load", function()
      {
        try
        {
          let long_key = reader.result;
          let crypto_key = crypto.createCipher("aes-128-cbc", long_key);
          let result = crypto_key.update(app.data.left_window_text, "utf-8", "hex");
          result += crypto_key.final("hex");
          app.data.right_window_text = result;
        }
        catch(error)
        {
          app.data.error_log = "Failed to encrypt the message";
        }
      }, false);

      reader.readAsDataURL(app.data.image_file);
    },

    decrypt: function()
    {
      let crypto = require('crypto')
      let reader = new FileReader();

      if(app.data.left_window_text == "")
      {
        app.data.error_log = "Missing text for decryption";
        return;
      }
      else if(app.data.image_file == undefined)
      {
        app.data.error_log = "Missing image key for decryption";
        return;
      }
      else
      {
        app.data.error_log = "";
      }

      reader.addEventListener("load", function()
      {
        try
        {
          let long_key = reader.result;
          let crypto_key = crypto.createDecipher("aes-128-cbc", long_key);
          let result = crypto_key.update(app.data.left_window_text, "hex", "utf8");
          result += crypto_key.final("utf8");
          app.data.right_window_text = result;
        }
        catch(error)
        {
          app.data.error_log = "Failed to decrypt the message";
        }
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