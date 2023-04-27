<template>
  <div class="container-fluid">
    <br />
    <h3 style="color: black">
      <div class="row">
        <div class="col-md-12">
          <h3>REGISTER</h3>
          <form role="form">
            <div class="form-group">
              <label for="exampleInputFirstname"> First name </label>
              <input type="Firstname" class="form-control" id="Firstname" />
            </div>
            <div class="form-group">
              <label for="exampleInputLastname"> Last name </label>
              <input type="Lastname" class="form-control" id="Last name" />
            </div>
            <div class="form-group">
              <label for="exampleInputUsername "> User name </label>
              <input type="Username " class="form-control" id="Username " />
            </div>
            <div class="form-group">
              <label for="exampleInputEmail1"> Email </label>
              <input
                type="email"
                class="form-control"
                id="exampleInputEmail1"
              />
            </div>
            <div class="form-group">
              <label for="exampleInputPassword1"> Password </label>
              <input
                type="password"
                class="form-control"
                id="exampleInputPassword1"
              />
            </div>

            <button type="submit" class="btn btn-primary mt-3">Submit</button>
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
