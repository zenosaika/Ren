<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-4">
          <div class="jelly-card" style="margin-right: 2px; overflow: auto;">
                <div v-for="user in users" :key="user.id" class="jelly-profile">
                    <div class="row" style="margin: 8px;">
                        <div class="col-3">
                            <img :src=user.image class="rounded-circle" width="55px" height="auto">
                        </div>
                        <div class="col-9">
                            <p style="margin:0px; font-size: 18px; font-weight:500">{{ user.name }}</p>
                            <p style="margin:0px; font-size: 12px">{{ user.package }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-8">
            <div class="jelly-card" style="margin-left: 2px">
                <div class="jelly-chatbox">
                    <div v-for="(message, i) in messages" :key="i" class="jelly-message" style="margin: 8px;">
                        <div class="row">
                            <div class="col-1">
                                <img :src=message.image class="rounded-circle" width="35px" height="auto">
                            </div>
                            <div class="col-11">
                                <p style="margin:0px; font-size: 14px; font-weight:500">{{ message.name }}</p>
                                <p v-for="(each_message, j) in message.body" :key="j" style="margin:0px; font-size: 14px; font-weight:300">{{ each_message }}</p>
                        </div>
                    </div>
                    </div>
                </div>
                <div style="display:flex; width:100%">
                    <input type="text" class="form-control jelly-input" placeholder="" aria-label="message" aria-describedby="basic-addon2">
                    <button class="btn btn-outline-secondary jelly-button" type="button" style="margin-left:15px">Send &#128172;</button>
                </div>
            </div>
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
                {id:5, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:6, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:7, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:8, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:9, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:10, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:11, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:12, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
                {id:13, name:'Hitori Bocchi', package:'Slime Plan', image:'images/bocchi.jpeg'},
            ],
            messages: [
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!', 'El Psy Congroo!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!', 'หวัดดี']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
                {name:'Hitori Bocchi', image:'images/bocchi.jpeg', body:['Pure Pure Miracle!']},
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
  border: 1px solid rgba(255, 255, 255, 0.15);
  margin-bottom: 15px;
  width: 100%;
  min-height: 75px;
}

.jelly-input {
    border-radius: 20px;
    border: 2px solid rgba(255, 255, 255, 0.15);
    background: transparent;
    color: #ccc;
}

.jelly-input:focus {
    border-radius: 20px;
    border: 2px solid rgba(255, 255, 255, 0.30);
    background: transparent;
    color: #ccc;
}

.jelly-button {
    border-radius: 20px;
    border: 2px solid rgba(255, 255, 255, 0.15);
    background: transparent;
    color: #ccc;
    white-space: nowrap;
}

.jelly-chatbox {
    display:flex; 
    width:100%; 
    height:90%; 
    overflow: auto;
    margin-bottom: 15px;
    flex-direction: column-reverse;
}
</style>
