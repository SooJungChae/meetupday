<template>
  <article class="wrap">
    <section>
      <div>
        url:
        <input nam="url" />
        <button>copy</button>
      </div>
      <div>
        사용자:
        <label>test</label>
      </div>
      <div>
        <button @click="sendKakaoLink">카카오톡 링크 보내기</button>
      </div>
      <div>
        <h3>소셜 로그인</h3>
        <button @click="loginFirebase()">구글 로그인 하기</button><br/>
        <button @click="loginFacebook()">페이스북 로그인 하기</button><br/>
        안녕, <input type="text" :value="userName">
      </div>
    </section>
    <section class="calendar-wrap">
      <div class="calendar">
      </div>
      <div class="calendar" @mousedown="startDrag" @mouseup="stopDrag">
        <!--ul*6>li.day$*7>button[click="toggleDay"]-->
        <ul>
          <li class="day1">Sun</li>
          <li class="day2">Mon</li>
          <li class="day3">Tue</li>
          <li class="day4">Wed</li>
          <li class="day5">Thu</li>
          <li class="day6">Fri</li>
          <li class="day7">Sat</li>
        </ul>
        <ul v-for="(weeks, weekIndex) in 6" :key="weeks">
          <li v-for="dayinweek in 7"
              :key="dayinweek"
              :class="{select: select}"
          >
            <day :value="(7 * weekIndex) + dayinweek"
                 @mouseenter="enter"
                 :dragging="dragging"
                @set="setDrag"
            ></day>
          </li>
        </ul>
      </div>
      <div class="calendar"></div>
    </section>
    <section>
      <div>
        참여자:
      </div>
      <div>
        총 0명
      </div>
    </section>
  </article>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Day from "../components/calendar/Day";
import firebase from 'firebase';
import { mapGetters } from 'vuex';

export default {
  components: {
    Day,
    Logo
  },
  data () {
    return {
      select: false,
      dragging: false,
      email: 'naanace@naver.com',
      db: ''
    }
  },
  computed: {
    ...mapGetters({
      userName: 'user/name'
    })
  },
  beforeMount () {
    let config = {
      apiKey: "AIzaSyDN0uvqEL-NzJm4WLxCF5c0svOyCad0pl0",
      authDomain: "meetupday.firebaseapp.com",
      databaseURL: "https://meetupday.firebaseio.com",
      projectId: "meetupday",
      storageBucket: "meetupday.appspot.com",
      messagingSenderId: "304960642409"
    };
  
    if (!firebase.apps.length) {
      firebase.initializeApp(config);
    }
  },
  methods: {
    loginFirebase () {
      const provider = new firebase.auth.GoogleAuthProvider();
  
      this.signInWithPopup(provider);
    },
    loginFacebook () {
      const provider = new firebase.auth.FacebookAuthProvider();
  
      this.signInWithPopup(provider);
    },
  
    signInWithPopup (provider) {
      firebase.auth().signInWithPopup(provider)
        .then((result) => {
          const user = result.user;
          this.$store.dispatch('user/setName', user.displayName);
        
        })
        .catch((error) => {
          console.error(error);
        });
    },
  
    // TODO ~ 카카오톡으로 링크를 보내면.
    // 카카오톡에서 링크로 들어오고
    // 사용자 정보를 가저와서 사용자를 입력한다.

    enter (e) {
      if (this.dragging) {
        console.log('enter');
      }
    },
    startDrag () {
      this.dragging = true;
    },
    stopDrag () {
      // select 된걸 저장한다.
      this.dragging = false;
      firebase.database().ref('users/' + this.userName).set({
        username: this.userName,
        email: this.email,
        selectedDays: {
          2019: {
            4: [1, 2, 3]
          }
        }
      });
    },
    setDrag ({ index, value }) {
      // TODO ~ 기록한다.
      console.log(index, value);
    },
    sendKakaoLink () {
      if (!Kakao.Auth) {
        Kakao.init('5cccc96ec27bdf694910e2cf25dacb3c');
      }
      Kakao.Link.sendDefault({
        objectType: 'feed',
        content: {
          title: 'meetupday',
          description: 'kakao link send',
          imageUrl: 'http://mud-kage.kakao.co.kr/dn/Q2iNx/btqgeRgV54P/VLdBs9cvyn8BJXB3o7N8UK/kakaolink40_original.png',
          link: {
            mobileWebUrl: 'http://localhost:3000',
            webUrl: 'http://localhost:3000'
          }
        },
        buttons: [
          {
            title: '웹으로 보기',
            link: {
              mobileWebUrl: 'http://localhost:3000',
              webUrl: 'http://localhost:3000'
            }
          }
        ]
      });
    }
  }
}
</script>

<style lang="scss">

html, body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

ul, li {
  list-style: none;
  margin: 0;
  padding: 0;
}

article {
  height: 100%;
  display: flex;
  flex-direction: column;
}

section {
  flex: 1;
  border: 1px solid red;

  &.calendar-wrap {
    height: 400px;
    display: flex;

    .calendar {
      flex: 1;
      display: flex;
      flex-direction: column;

      ul {
        flex: 1;
        display: flex;

        li {
          flex: 1;

          .day-wrap {
            div {
              height: 100%;
              border: 1px solid red;
            }

            &.active {
              background-color: red;
            }
          }

        }
      }
    }
  }
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
