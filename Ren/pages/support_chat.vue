<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-4">
          <div class="jelly-card" style="margin-right: 2px">
                <div class="jelly-profile" v-for="user in users" :key="user.id">
                    <div class="row" style="margin: 8px;">
                        <div class="col-3">
                            <img :src=user.image class="rounded-circle" width="55px" height="auto">
                        </div>
                        <div class="col-9">
                            <p style="margin:0px; font-size: 18px">{{ user.name }}</p>
                            <p style="margin:0px; font-size: 12px">{{ user.package }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-8">
          <div class="jelly-card" style="margin-left: 2px">test</div>
        </div>
      </div>
    </div>
    <vue-particles color="#dedede"></vue-particles>
  </div>
</template>

<script>
export default {
    data() {
        return {
            users: [
                {id:1, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:2, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:3, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:4, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
            ]
        }
    }
}
</script>

<style>
body {
  color: #ccc;
  margin: 0px;
  padding: 0px;
}

.container {
    position: absolute;
    left: 50px;
    right: 50px;
    z-index: 999;
}

.jelly-card {
  backdrop-filter: blur(4px) saturate(140%);
  -webkit-backdrop-filter: blur(4px) saturate(140%);
  background-color: rgba(17, 25, 40, 0.1);
  border-radius: 20px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  margin: 50px;
  padding: 15px;
  height: 650px;
  display: flex;
  justify-content: center;
  align-content: flex-start;
  flex-wrap: wrap;
}

.jelly-profile {
  border-radius: 20px;
  border: 2px solid rgba(255, 255, 255, 0.15);
  margin-bottom: 15px;
  width: 100%;
  min-height: 75px;
}

.jelly-message {
  backdrop-filter: blur(4px) saturate(140%);
  -webkit-backdrop-filter: blur(4px) saturate(140%);
  background-color: rgba(17, 25, 40, 0.1);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.125);
  margin: 50px;
  padding: 50px;
  height: 650px;
}
</style>
