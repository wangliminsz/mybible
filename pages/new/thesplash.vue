
<template>

  <div class="text-gray-900 font-bold font-italic font-Comfortaa">

    <header class="mb-10">

      <div class="container">

        <div class="nav">

          <!-- <h2><i class="fas fa-camera"
               style="color:orange; margin:3px"></i>Unsplash API Demo</h2> -->

          <div class="search-box">
            <input type="text"
                   id="input"
                   placeholder="Search..."
                   v-model="theQueryUrl"
                   @keyup.enter="loadImg"><i @click="loadImg"
               class="fas fa-search"></i>

          </div>

          <div class="m-3 flex-none">
            <button class="px-3 py-1 bg-blue-500 border rounded shadow-2xl text-white text-sm flex-none"
                    @click="myimgpage(theImgUrl)"><a href="/new/thetext">
                OK Confirm
              </a></button>
          </div>

        </div>

      </div>
    </header>

    <div class="w-full m-auto grid grid-cols-3 gap-4 p-5"
         v-if="imgArray[0]">
      <div class="flex justify-around m-2 p-2"
           v-for="(i,index) in imgArray"
           :key="index">

        <div flex
             v-model="imgSelected">

          <img :src="i"
               @dblclick="recordUrl(i,index)"
               class="imgcss"
               :style="imgStyle(index)"
               alt="" />

        </div>
      </div>

    </div>

  </div>

</template>

<script>
//import { mapState } from 'vuex'
import { mapMutations } from 'vuex'
//import { mapActions, mapGetters } from 'vuex'

export default {
  head: {
    link: [
      {
        rel: 'stylesheet',
        href: 'https://cdn.bootcdn.net/ajax/libs/font-awesome/5.15.3/css/all.min.css',
      },
    ],
  },

  computed: {},

  data() {
    return {
      theQueryUrl: '',
      theImgUrl: '',
      image: '',
      imgArray: [],
      imgSelected: 100,
    }
  },

  //   created() {
  //     this.loadImg()
  //   },

  methods: {
    // 映射store.mutations
    ...mapMutations({
      increment: 'increment',
      myimgpage: 'myimgpage',
    }),

    imgStyle(args1) {
      //   console.log('index----' + args1)
      //   console.log('imgSelected' + this.imgSelected)

      if (args1 === this.imgSelected) {
        return {
          opacity: '50%',
          //padding: '5px',
        }
      }
    },

    recordUrl(args1, args2) {
      //alert('Gotit' + args2)

      this.theImgUrl = args1
      this.imgSelected = args2
      //window.open(this.theImgUrl, '_blank')
      //window.open(this.theImgUrl)
    },

    removeImages() {
      this.imgArray = []
      this.imgSelected = 100
    },

    random(min, max) {
      return Math.floor(Math.random() * (max - min)) + min
    },

    loadImg() {
      let imgRandom = 0
      let url = ''

      this.removeImages()

      //alert('Hello loadImg' + '----' + this.theQueryUrl)

      imgRandom = this.random(1, 100)

      if (imgRandom <= 50) {
        url = 'https://api.unsplash.com/search/photos/?query=' + this.theQueryUrl + '&per_page=18&client_id=5T916LLmUG9kAW6lhMY3iAKq-9H4zL0WxrpapsPy7nM'
      } else if(imgRandom <= 100) {
        url = 'https://api.unsplash.com/search/photos/?query=' + this.theQueryUrl + '&per_page=18&client_id=2th_gqNwnvgcfb0ikWBWWlvFQlF5O9rrurV7GF7KAxI'
      }

      //5T916LLmUG9kAW6lhMY3iAKq-9H4zL0WxrpapsPy7nM
      //2th_gqNwnvgcfb0ikWBWWlvFQlF5O9rrurV7GF7KAxI

      //this.theQueryUrl = ''

      fetch(url)
        .then((response) => {
          //console.log(response);

          if (response.ok) return response.json()
          else console.log(response.status)
        })

        .then((json) => {
          //console.log(json.results[0].urls.raw)
          //this.image = json.results[0].urls.raw

          let i
          for (i = 0; i < json.results.length; i++) {
            this.imgArray.push(json.results[i].urls.raw)
          }
        })
    },
  },
}
</script>

<style scoped>
body {
  font-family: 'Comfortaa', cursive;
  background-color: black;
  color: white;
}

header {
  border-bottom: 1px solid orange;
}

.container {
  width: 90%;
  margin: auto;
}

.nav {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 25px 0;
}

.nav h2 {
  font-size: 2rem;
}

.search-box {
  position: relative;
  width: 350px;
}

.search-box input {
  box-sizing: border-box;
  width: 100%;
  font-size: 1rem;
  padding: 8px;
  border-radius: 6px;
  outline: none;
  border: 1px solid lightgray;
}

input:focus {
  box-shadow: 0 0 5px orange;
  border: 1px solid orange;
}

.search-box i {
  color: black;
  position: absolute;
  top: 25%;
  right: 4%;
  transition: 1.5s;
}

.search-box i:hover {
  color: orange;
}

.imgcss {
  width: 450px;
  height: 280px;
  margin-top: 15px;
  background-position: 50% 50%;
  background-size: cover;
  border-radius: 15px;
}

.imgcss1 {
  width: 450px;
  height: 280px;
  margin-top: 15px;
  background-position: 50% 50%;
  background-size: cover;
  opacity: 50%;
  border-radius: 15px;
}

@media (max-width: 768px) {
  .imgcss {
    width: 100%;
  }
  .nav {
    justify-content: center;
  }
  .nav h2 {
    padding: 5px 0;
  }
}

@media (max-width: 480px) {
  .nav h2 {
    text-align: center;
    font-size: 1.5rem;
  }
  .search-box {
    width: 80%;
    margin: auto;
  }
  .search-box input {
    font-size: 0.7rem;
  }
}
</style>>