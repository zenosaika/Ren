<template>
  <div class="container-fluid">
    <div class="padleft">
      <div class="padtop">
        <p class="homepage_subtitle">PYHTONFLIX ORIGINAL</p>
      </div>
      <h1 style="color: white"><b class="movie_title">THE 220's CLASS</b></h1>
      <p class="stats">602.5 K views - 3 months ago - 2 Seasons</p>
      <div class="description">
        <p style="color: lightgrey">
          When a subject required students to work together and forced them
          <br />to group up causing loads of works to be done uppon the students
          who were<br />
          at the initial of the final test of their semester. Will they be able
          to survive<br />throghtout these works and test? Find out on this
          show!
        </p>
      </div>
      <div class="author">
        <i class="author"
          >ChickenAstronaut Heart James MewP Dew Classroom Shows</i
        >
      </div>
      <div class="title"><b>Popular on Pythonflix</b></div>
      <div class="container">
        <div class="row">
          <div
            v-for="(video, i) in videos"
            :key="i"
            class="col-12 col-md-6 col-lg-4"
          >
            <a :href="video.url"
              ><img :src="video.thumbnail" class="card-img-top crop"
            /></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
export default Vue.extend({
  layout: 'mylayout',
  async asyncData({ $axios }) {
    const videos = await $axios
      .$get('https://eo9ic0-8080.csb.app/api/get/video')
      .then((res) => {
        const data = res.data
        for (let i = 0; i < data.length; i++) {
          const temp = data[i].url.split('/')
          data[i].thumbnail = `https://img.youtube.com/vi/${
            temp[temp.length - 1]
          }/hqdefault.jpg`
        }
        return res.data
      })
    return {
      videos,
    }
  },
  data() {
    const videos = [
      {
        url: 'https://www.youtube.com/watch?v=zUcc4vW-jsI&ab_channel=ByteGrad',
      },
      {
        url: 'https://www.youtube.com/watch?v=zUcc4vW-jsI&ab_channel=ByteGrad',
      },
      {
        url: 'https://www.youtube.com/watch?v=zUcc4vW-jsI&ab_channel=ByteGrad',
      },
    ]
    return {
      videos,
    }
  },
})
</script>

<style>
body {
  background-image: url('https://wallpaperaccess.com/full/133206.jpg') !important;
  background-color: #cccccc;
  background-repeat: no-repeat;
  background-size: 100%;
}

h1 {
  font-family: 'Lato', sans-serif;
  margin-top: 0;
  margin-bottom: 0;
  font-size: 50px;
  color: white;
}

h2 {
  font-family: 'Lato', sans-serif;
  margin-top: 0;
  margin-bottom: 0;
  color: white;
}

p,
i,
b {
  font-family: 'Lato', sans-serif;
  color: white;
}

.title {
  font-family: 'Lato', sans-serif;
  font-size: 30px;
  margin-top: 40px;
  margin-bottom: 40px;
  color: white;
}

.description {
  font-family: 'Lato', sans-serif;
  margin-top: 0px;
  margin-bottom: 10px;
  color: grey;
}

.stats {
  font-family: 'Lato', sans-serif;
  margin-top: 10px;
  margin-bottom: 10px;
  color: grey;
}

.padleft {
  margin-left: 70px;
}

.padtop {
  margin-top: 70px;
}

.author {
  margin-top: 10px;
  margin-bottom: 100px;
  color: grey;
}

img {
  width: auto;
  height: 220px;
  overflow: hidden;
}
</style>
