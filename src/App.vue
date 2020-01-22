<template>
  <div id="app">
    <div class="container">
      <h1 class="mt-3">Insane profile card generator</h1>
      <div class="row mt-5">
        <div class="col-4 noprint">
          <div class="form-group">
            <label for="first-name">Avatar</label>
            <div class="input-group">
              <input type="file" ref="file" accept="image/*" @change="fileUpload" multiple>
            </div>
          </div>
          <div class="form-group">
            <label for="name">Name</label>
            <div class="input-group">
              <input type="text" class="form-control" id="name" v-model="name" />
            </div>
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <div class="input-group">
              <input type="text" class="form-control" id="email" autoComplete="email" v-model="email" />
            </div>
          </div>
          <div class="form-group">
            <label for="role">Role</label>
            <div class="input-group">
              <input type="text" class="form-control" id="role" v-model="role" />
            </div>
          </div>
          <div class="form-group">
            <label for="role">Bio</label>
            <div class="input-group">
              <input type="text" class="form-control" id="role" v-model="bio" />
            </div>
          </div>
          <legend>Icons</legend>
          <div class="togglebox">
            <input type="checkbox" id="togglebox-example-1" v-model="icons.slack" />
            <label for="togglebox-example-1">Slack</label>
          </div>
          <div class="togglebox">
            <input type="checkbox" id="togglebox-example-2" v-model="icons.phone" />
            <label for="togglebox-example-2">Phone</label>
          </div>
          <div class="togglebox">
            <input type="checkbox" id="togglebox-example-3" v-model="icons.email" />
            <label for="togglebox-example-3">Email</label>
          </div>
          <legend>Theme</legend>
          <div class="radio">
            <input type="radio" id="radio-example-1" name="theme" value="swedbankpay" v-model="theme" />
            <label for="radio-example-1">Swedbank Pay</label>
          </div>
          <div class="radio">
            <input type="radio" id="radio-example-2" name="theme" value="payex" v-model="theme" />
            <label for="radio-example-2">PayEx</label>
          </div>
        </div>
        <div class="col-4">
          <button class="btn-lg btn noprint mb-2" onclick="window.print();return false;">Print</button>
          <div class="card card-primary" :class="{'card-payex': theme == 'payex'}" style="max-width: 240px;">
            <div class="card-img">
              <img :src="avatar" alt />
              <div class="icon-container">
                <img
                  src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fs3.amazonaws.com%2Fapollo-docs-1.x%2Fimages%2Fslack.png&f=1&nofb=1"
                  v-if="icons.slack">
                <img
                  src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcdn0.iconfinder.com%2Fdata%2Ficons%2Ftraffic%2F500%2Fva0032-512.png&f=1&nofb=1"
                  v-if="icons.phone">
                <img
                  src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcdn3.iconfinder.com%2Fdata%2Ficons%2Fminiglyphs%2F500%2F063-512.png&f=1&nofb=1"
                  v-if="icons.email">
              </div>
            </div>
            <header class="card-header">
              <h3>{{ name }}</h3>
              <p> {{ email }} </p>
              <p> {{ role }} </p>
            </header>
            <div class="card-body">
              <p>{{ bio }}</p>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data: () => {
      return {
        avatar: 'https://picsum.photos/300/?random',
        name: 'Nicholas Cage',
        email: 'nicholas.cage@theone.com',
        role: "Some role",
        bio: 'Back in my day...',
        theme: "swedbankpay",
        tempFile: null,
        icons: {
          slack: false,
          phone: false,
          email: false
        }
      };
    },
    methods: {
      fileUpload(event) {
        // eslint-disable-next-line
        console.log(event.target.files);

        this.tempFile = event.target.files[0];

        let reader = new FileReader();

        reader.addEventListener("load", function () {
          this.avatar = reader.result;
        }.bind(this), false);

        if (this.tempFile) {
          if (/\.(jpe?g|png|gif)$/i.test(this.tempFile.name)) {
            reader.readAsDataURL(this.tempFile);
          }
        }
      }
    }
  }
</script>

<style>
  @media print {
    .noprint {
      display: none;
    }
  }

  .card .card-img {
    position: relative;
  }

  .card .card-img img {
    object-fit: contain;
  }

  .card-payex.card.card-primary {
    background-color: #fff;
  }

  .card-payex.card.card-primary .card-header {
    border-top: 7px solid #2da944;
  }

  .card-payex.card.card-primary .card-header:after {
    content: none;
  }

  .icon-container {
    position: absolute;
    right: 0;
    top: 0;
    padding: 6px;
    background-color: #ffffffa3;
  }

  .card .card-img .icon-container img {
    height: 28px;
    width: 28px;

  }
</style>