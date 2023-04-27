<template>
  <div class="container-fluid">
    <br />
    <h3 style="color: black">
      <div class="row">
        <div class="col-md-12">
          <form role="form">
            <div class="form-group">
              <h1>LOGIN</h1>
              <div class="form-floating mb-3">
                <input
                  type="email"
                  class="form-control"
                  id="floatingInput"
                  placeholder="name@example.com"
                />
                <label for="floatingInput" style="font-size: 16px">Email</label>
              </div>
              <div class="form-floating">
                <input
                  type="password"
                  class="form-control"
                  id="floatingPassword"
                  placeholder="Password"
                />
                <label for="floatingPassword" style="font-size: 16px"
                  >Password
                </label>
              </div>
              <button type="LOGIN" class="btn btn-primary w-100 mt-3">
                LOGIN
              </button>
            </div>
          </form>
        </div>
      </div>
    </h3>
  </div>
</template>

<script lang="js">
import Vue from 'vue'

export default Vue.extend({
  layout: 'mylayout',

})
</script>

<style>
body {
  background-image: url('https://media.discordapp.net/attachments/922537694792400986/1100290475426058330/IMG_0714.png?width=1880&height=936');
}

.container-fluid {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  border-radius: 10px;
  background: white;
}

.btn {
  background-color: red;
}
</style>
