<template>
  <q-page class="relative-position">
    <q-scroll-area class="absolute fullscreen">
      <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
        <div class="col">
          <q-input autogrow class="new-qweet" bottom-slots v-model="newQweetContent" placeholder="What's Happening?"
            counter maxlength="280">
            <template v-slot:before>
              <q-avatar size="xl">
                <img src="https://www.gravatar.com/avatar/a3271a565b14ec4709dba65e227527b4">
              </q-avatar>
            </template>
          </q-input>
        </div>
        <div class="col col-shrink">
          <q-btn @click="addNewQweet" :disable="!newQweetContent" unelevated no-caps rounded color="primary" label="Qweet"
            class="q-mb-lg" />
        </div>
      </div>
      <q-separator size="7px" color="grey-3" class="divider" />
      <transition-group appear enter-active-class="animated fadeIn slow" leave-active-class="animated fadeOut slow">
        <q-list class="qweet q-py-md" v-for="qweet in qweets" :key="qweet.date">
          <q-item>
            <q-item-section avatar top>
              <q-avatar size="xl">
                <img src="https://www.gravatar.com/avatar/a3271a565b14ec4709dba65e227527b4">
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label class="text-subtitle1">
                <strong>Aryan Soni</strong>
                <span class="text-grey-7"> &bull; @krypto_xenon &bull; {{ qweet.date }} </span>
              </q-item-label>
              <q-item-label class="qweet-content text-body1">
                {{ qweet.content }}
              </q-item-label>
              <div class="row justify-between qweet-icons q-mt-sm">
                <q-btn flat round color="grey" icon="far fa-comment" size="sm" />
                <q-btn flat round color="grey" icon="fas fa-retweet" size="sm" />
                <q-btn flat round color="grey" icon="far fa-heart" size="sm" />
                <q-btn @click="deleteQweet(qweet)" flat round color="grey" icon="fas fa-trash" size="sm" />

              </div>
            </q-item-section>
          </q-item>
        </q-list>
      </transition-group>
    </q-scroll-area>
  </q-page>
</template>

<script>
// import { formatDistance } from 'date-fns'
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data() {
    return {
      newQweetContent: "",
      qweets: [
        {
          content: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam praesentium, ipsam quod quo eveniet voluptates dolore vero error sit explicabo dolorem laborum odio quibusdam! Suscipit iusto distinctio adipisci sequi commodi.",
          date: 1688833446780
        },
        {
          content: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam praesentium, ipsam quod quo eveniet voluptates dolore vero error sit explicabo dolorem laborum odio quibusdam! Suscipit iusto distinctio adipisci sequi commodis.",
          date: 1688833469281
        }
      ]
    }
  },
  methods: {
    addNewQweet() {
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now()
      }
      this.qweets.unshift(newQweet) //push() adds the qweet to the last so use unshift()
      this.newQweetContent = ''
    },
    deleteQweet(qweet) {
      let dateToDelete = qweet.date
      let index = this.qweets.findIndex(qweet => qweet.date === dateToDelete)
      this.qweets.splice(index, 1)
    }
  }
  // filters: {
  //   relativeDate(value) {
  //     return formatDistance(value, new Date(), { addSuffix: true })
  //   }
  // }
})
</script>

<style lang="sass">
.new-qweet
  textarea
    font-size:19px
    line-height: 1.2 !important
.divider
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4
.qweet:not(:first-child)
  border-top: 1px solid rgba(0, 0, 0, 0.12)
.qweet-content
  white-space: pre-line !important
.qweet-icons
  margin-left: -5px
</style>