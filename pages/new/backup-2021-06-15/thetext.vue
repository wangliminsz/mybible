<template>

  <div class="flex">

    <div class="m-3 flex-none">
      <button class="px-3 py-1 bg-blue-500 border rounded shadow-2xl text-white text-sm flex-none"
              @click="mytxtpage(myContent)"><a href="/new/thesplash">
          OK Confirm
        </a></button>
    </div>

    <div class="m-10 p-10 justify-center">

      <textarea rows="15"
                cols="80"
                autofocus
                class="m-3 p-10 border-2 border-yellow border-solid bg-gray-100 text-left"
                v-model="theTxtContent">
       </textarea>

    </div>

  </div>

</template>

<script>
import { mapState } from 'vuex'
import { mapMutations } from 'vuex'
import { mapActions, mapGetters } from 'vuex'

export default {
  data: function () {
    return {

      myChapter: '',
      myText: '',

      myContent: {},
      theTxtContent: '',

    }
  },

  mounted: function () {
    this.thisMyText()
  },

  computed: {
    // 映射store.state
    ...mapState({
      theText: (state) => state.sessionStorage.storedVerse,
      theBk: (state) => state.sessionStorage.storedBk,
      theVer: (state) => state.sessionStorage.storedVer,
    }),
  },

  methods: {
    // 映射store.mutations
    ...mapMutations({
      increment: 'increment',
      mytxtpage: 'mytxtpage',
    }),

    ...mapActions({}),

    thisMyText() {


      for (let i = 0; i < this.theText.length; i++) {
        let theStr = this.theText[i].theVerse.replace(/\n|\r/g, ' ')

        if (
          i == 0 ||
          (i > 0 &&
            this.theText[i].bkNumber == this.theText[i - 1].bkNumber &&
            this.theText[i].chNumber == this.theText[i - 1].chNumber + 1)
        ) {
          this.myText = this.myText + theStr
        } else {
          this.myText = this.myText + ' … ' + theStr
        }
      }

      for (let i = 0; i < this.theText.length; i++) {
        if (i == this.theText.length - 1) {
          this.myChapter =
            this.myChapter +
            this.theText[i].bkNumber +
            ':' +
            this.theText[i].chNumber
        } else {
          this.myChapter =
            this.myChapter +
            this.theText[i].bkNumber +
            ':' +
            this.theText[i].chNumber +
            ' | '
        }
      }

      //this.myContent = this.myText + '\n\n' + this.theBk + ' ' + this.myChapter

      let key1 = 'keyBk'
      let key2 = 'keyVer'
      let key3 = 'keyCh'
      let key4 = 'keyContent'
      
      //let key5 = 'keyContentThai'
  
      this.myContent[key1] = this.theBk
      this.myContent[key2] = this.theVer
      this.myContent[key3] = this.theBk + ' ' + this.myChapter
      this.myContent[key4] = this.myText

      this.theTxtContent = this.myContent[key4]  + '\n\n' + this.myContent[key3] 

    },
  },
}
</script>

<style>
</style>