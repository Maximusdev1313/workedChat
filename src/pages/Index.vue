<template>
  <q-page class="relative-position">
    <div class="row items-end q-col-glutter-md">
        <div class="col">
           <div class="row items-end q-col-glutter-md inputs " >
         <div class="col">
          <q-input
          bottom-slots
          v-model="name"
          label="Ismingiz"
          counter
          maxlength="280"
          class="inputForTweet q-pr-md q-pl-sm newTweet"
          autogrow

          >

          <template v-slot:before>
            <q-avatar size="md">
              <q-icon name="person" size="md"/>
            </q-avatar>
          </template>

          <template v-slot:append>
            <!-- <q-icon v-if="newTweet !== ''" name="close" @click="newTweet = ''" class="cursor-pointer" /> -->

          </template>

        </q-input>
         <q-input
          bottom-slots
          v-model="massage"
          label="Savol bering"
          counter
          maxlength="280"
          class="inputForTweet q-pr-md q-pl-xl newTweet "
          autogrow
          v-if="name.length >= 3"
          >
           <template v-slot:append>
            <q-icon v-if="massage !== ''" name="close" @click="massage = ''" class="cursor-pointer" />

          </template>
          </q-input> 
        </div>
        <div class="col col-shrink">

             <q-btn
              @click="addTweet"
              :disable="!addTweet"
              color="primary"
              class="q-mb-md q-mr-md"
              label="Yuborish"
              rounded
              unelevated
              no-caps
              /> 

        </div>
      </div>
      <q-separator
      size="10px"
      color="grey-2"
      class="devider"
      />
        </div>
      </div>
    <q-scroll-area class="absolute full-height full-width">
       
      
      <!-- tweet lists -->
        <q-list class="relative">
          <q-item class="q-mt-md" v-for="tweet in tweets" :key="tweet.id">
           <q-item-section avatar top>
              <q-avatar>
                <q-icon name="person" size="lg" color="grey"/>
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label class="text-weigth-bold text-subtitle1">
                <span class="text-grey row">
                  @{{tweet.name}}
                  <q-space></q-space>
                  <!-- <br class="lt-md"> -->
                  <span class="text-overline ">
                      {{momentDate}}
                  </span>
                </span>
                </q-item-label>
              <q-item-label class="inputForTweet">
                {{tweet.massage}}
              </q-item-label>                                 
              <q-separator
                size="2px"
                color="grey-2"
                class="q-mt-md"
                />
              <div class="row justify-between">
                <!-- <q-btn
                color="grey"
                icon="far fa-comment"
                size="sm"
                flat4
                round
                ></q-btn> -->
                <!-- <q-btn
                color="grey"
                icon="fas fa-retweet"
                size="sm"
                flat
                round
                ></q-btn> -->
                <!-- <q-btn
                @click="toggleLiked(tweet)"
                :color="tweet.liked ? 'pink' : 'grey' "
                :icon="tweet.liked ? 'fas fa-heart' : 'far fa-heart'"
                size="sm"
                flat
                round
                >
                &bull; {{tweet.likes}}
                </q-btn>

                <q-btn
                color="grey"
                icon="fas fa-trash"
                size="sm"
                flat
                round
                @click="removeTweet(tweet)"
                ></q-btn> -->
              </div>


            </q-item-section>
          </q-item>




      </q-list>
      
    
    </q-scroll-area>
   

  </q-page>
</template>

<script>
import { defineComponent, onMounted,ref } from 'vue';
import axios from 'axios'
import Pusher from 'pusher-js'
// import { formatDistance} from 'date-fns'
import moment from 'moment'
export default defineComponent({
  name: 'Index',
  
  setup(){
    const openQuestionPanel = ref(false)
    const name  = ref('')
    const massage = ref('')
    const tweets = ref([])
    const date = ref(Date.now())
    // const moment = ref('')
    const momentDate = ref('')
   
    onMounted(()=>{
       Pusher.logToConsole = false;

      const pusher = new Pusher('8ac282d8b5fbf6b803e7', {
        cluster: 'ap2'
      });

      const channel = pusher.subscribe('TweetMax-development');
      channel.bind('massage', data => {
        tweets.value.unshift(data);
    });

    })
    const addTweet = async ()=>{
      await fetch('http://maximusdev.pythonanywhere.com/api/', {
        
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
          name: name.value,
          massage: massage.value,
          date: date.value
        }) 
      })
      massage.value = ''
    }
     const getTweet = async ()=>{
      try {
        const res = await axios.get('http://maximusdev.pythonanywhere.com/api/')
        tweets.value = res.data
        tweets.value.reverse()
        const timeNow = moment(tweets.date).format('LLL');
        momentDate.value = timeNow
             }
      catch(err){
        console.log(err);
      }
    }

    setInterval(()=>{
      getTweet()
    }, 100)
   
    return{
       tweets,
       name,
       massage,
       addTweet,
       date,
       moment,

       momentDate,
       openQuestionPanel,
        toggleQuestionPanel(){
          openQuestionPanel.value = !openQuestionPanel.value
        },
         

       
    }
  }


})
</script>
<style lang="sass">
.inputForTweet
    white-space: pre-line
.newTweet
    textarea
      font-size: 16px
      line-height: 1.4 !important
.devider
    border-top: 1px solid
    border-bottom: 1px solid
    border-color: $grey-5
    margin-top: 50px
.inputs
   
    background-color: #fff
    height: auto
</style>
