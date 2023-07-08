<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
        <q-input autogrow class="new-qweet" bottom-slots v-model="newQweetContent" placeholder="What's Happening?" counter
          maxlength="280">
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://www.gravatar.com/avatar/a3271a565b14ec4709dba65e227527b4">
            </q-avatar>
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn :disable="!newQweetContent" unelevated no-caps rounded color="primary" label="Qweet" class="q-mb-lg" />
      </div>
    </div>
    <q-separator size="7px" color="grey-3" class="divider" />

    <q-list class="q-py-md" v-for="qweet in qweets" :key="qweet.date">
      <q-item>
        <q-item-section avatar top>
          <q-avatar size="xl">
            <img src="https://www.gravatar.com/avatar/a3271a565b14ec4709dba65e227527b4">
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1">
            <strong>Aryan Soni</strong>
            <span class="text-grey-7">@krypto_xenon</span>
          </q-item-label>
          <q-item-label class="qweet-content text-body1">
            {{ qweet.content }}
          </q-item-label>
          <div class="row justify-between qweet-icons q-mt-sm">
            <q-btn flat round color="grey" icon="far fa-comment" size="sm" />
            <q-btn flat round color="grey" icon="fas fa-retweet" size="sm" />
            <q-btn flat round color="grey" icon="far fa-heart" size="sm" />
            <q-btn flat round color="grey" icon="fas fa-trash" size="sm" />

          </div>
        </q-item-section>

        <q-item-section side top>
          <!-- {{ qweet.date | relativeDate }}  -->
        </q-item-section>
      </q-item>
    </q-list>

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
.qweet-content
  white-space: pre-line !important
.qweet-icons
  margin-left: -5px
</style>