<template>
  <v-container fluid>
    <v-row>
      <v-col cols="11" class="mx-auto">
        <v-card class="" style="padding:0; margin:0; border-radius:7%;">
          <v-img
            class="white--text"
            height="15vh"
            src="https://cdn.pixabay.com/photo/2016/05/11/13/20/keyboard-1385706_960_720.jpg"
            style="border-radius:10px; margin-top:2%;"
          >
            <v-card-title>채팅방</v-card-title>
          </v-img>
        </v-card>
      </v-col>
    </v-row>
    <v-row style="text-align:center; margin-top:5vh;">
      <v-col col="10" offset="1" >
        <!-- 채팅방이름 ,참여인원수변수 , 클릭이벤트 -->
        <div class="chatroomdiv">
          <h1 class="white--text">영화</h1>
        <v-card class="chatroom ">
          <v-img
            class="white--text"
            height="38vh"
            width="40vw"
            src="../assets/chatimg1.jpg"
            style="border-top-left-radius:20px; border-top-right-radius:20px;"
          >
          </v-img>
            <div class="d-inline-flex">
              <v-icon dark large class="icon">mdi-account-circle</v-icon>
              <h4>123{{chat1cnt}}</h4>
              <button type="button" @click="chat1">
                입장하기
              </button>
            </div>
        </v-card>
        </div>

        <div class="chatroomdiv">
          <h1 class="white--text">드라마</h1>
        <v-card class="chatroom" >
          <v-img
            class="white--text"
            height="38vh"
            width="40vw"
            src="../assets/chatimg2.jpg"
            style="border-top-left-radius:20px; border-top-right-radius:20px;"
          >
          </v-img>
            <div class="d-inline-flex">
              <v-icon dark large class="icon">mdi-account-circle</v-icon>
              <h4>123{{chat1cnt}}</h4>
              <button type="button" @click="chat2">
                입장하기
              </button>
            </div>
        </v-card>
        </div>

        <div class="chatroomdiv">
          <h1 class="white--text">TV프로그램</h1>
        <v-card class="chatroom" >
          <v-img
            class="white--text"
            height="38vh"
            width="40vw"
            src="../assets/chatimg3.jpg"
            style="border-top-left-radius:20px; border-top-right-radius:20px;"
          >
          </v-img>
            <div class="d-inline-flex">
              <v-icon dark large class="icon">mdi-account-circle</v-icon>
              <h4>123{{chat1cnt}}</h4>
              <button type="button" @click="chat3">
                입장하기
              </button>
            </div>
        </v-card>
        </div>

        <div class="chatroomdiv">
          <h1 class="white--text">애니</h1>
        <v-card class="chatroom" >
          <v-img
            class="white--text"
            height="38vh"
            width="40vw"
            src="https://t1.daumcdn.net/cfile/tistory/9917503E5AB207E12E"
            style="border-top-left-radius:20px; border-top-right-radius:20px;"
          >
          </v-img>
            <div class="d-inline-flex">
              <v-icon dark large class="icon">mdi-account-circle</v-icon>
              <h4>123{{chat1cnt}}</h4>
              <button type="button" @click="chat4">
                입장하기
              </button>
            </div>
        </v-card>
        </div>
      </v-col>
    </v-row>
    
    
    <!-- 채팅방 다이얼로그 -->
      <v-dialog v-model="dialog" persistent width="500">
      <v-card dark>
        <v-card-title class="text-h5 lighten-2">
          {{flagName}}
        </v-card-title>

        <v-card-text>
          <!-- <label>내용</label> -->
          <md-field>
          <md-textarea class="ta" v-model="textarea" disabled v-auto-scroll-bottom rows="10" row-height="50"></md-textarea>
          </md-field>
          <!-- <label>입력</label> -->
          <v-text-field
              label="내용 입력 후 Enter"
              v-model="message"
              @keyup.enter="sendMessage()"
              />
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="white" text @click="exitRoom">
            나가기
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog> 
  </v-container>

</template>


<script>
import axios from 'axios'
export default {
    created() {
        var vm = this;
        axios.get('/auth/info')
            .then(res => {
            // console.log("front :: " , res);
            vm = res.data;
            this.authName = vm.name;
            this.authEmail = vm.email;
            this.authId = vm._id;
            })
            .catch(err => {
            // console.log(err);
        });
        //  방 접속 알림
        this.$socket.on('noti_join_room', (res) => {
          this.textarea += "  SYSTEM : [" + res.authName + "] " + res.message + "\n"
          if(this.flag == 'chat1'){
            this.chat1cnt = res.cnt
            console.log('chat1 : ' + this.chat1cnt)
          }else if(this.flag == 'chat2'){
            this.chat2cnt = res.cnt
            console.log('chat2 : ' + this.chat2cnt)
          }else if(this.flag == 'chat3'){
            this.chat2cnt = res.cnt
            console.log('chat3 : ' + this.chat3cnt)
          }else if(this.flag == 'chat4'){
            this.chat2cnt = res.cnt
            console.log('chat4 : ' + this.chat4cnt)
          }
        });
        //  방 퇴장 알림
        this.$socket.on('noti_exit_room', (res) => {
          this.textarea += "  SYSTEM : [" + res.authName + "] " + res.message + "\n"
          if(this.flag == 'chat1'){
            this.chat1cnt = res.cnt
            console.log('chat1 : ' + this.chat1cnt)
          }else if(this.flag == 'chat2'){
            this.chat2cnt = res.cnt
            console.log('chat2 : ' + this.chat2cnt)
          }else if(this.flag == 'chat3'){
            this.chat3cnt = res.cnt
            console.log('chat3 : ' + this.chat3cnt)
          }else if(this.flag == 'chat4'){
            this.chat4cnt = res.cnt
            console.log('chat4 : ' + this.chat4cnt)
          }
        });
        //  방별 새로운 메세지 받아오기
        this.$socket.on('getMsg', (res) => {
          this.textarea += "[" + res.authName + "] " + res.message + "\n"
        });
        //  접속자 수 업데이트
        this.$socket.on('update', (res) => {
          this.chat1cnt = res.cnt1,
          this.chat2cnt = res.cnt2,
          this.chat3cnt = res.cnt3,
          this.chat4cnt = res.cnt4
        })
    },
  data () {
    return {
      dialog : false,
      roomName : '',
      authName : '',
      textarea: "",
      message: '',
      chat1cnt: null,
      chat2cnt: null,
      chat3cnt: null,
      chat4cnt: null,
      flag: '',
      flagName: ''
    }
  },
  methods: {
    chat1 () {
      this.dialog = true
      this.flag = 'chat1';
      this.flagName = '영화';
      this.roomName = 'chat1';
      this.$socket.emit('req_join_room', {
        roomName: this.roomName,
        authName: this.authName 
      });
    },
    chat2 () {
      this.dialog = true
      this.flag = 'chat2'
      this.flagName = '드라마';
      this.roomName = 'chat2';
      this.$socket.emit('req_join_room', {
        roomName: this.roomName,
        authName: this.authName
      });
    },
    chat3 () {
      this.dialog = true
      this.flag = 'chat3'
      this.flagName = 'TV프로그램';
      this.roomName = 'chat3';
      this.$socket.emit('req_join_room', {
        roomName: this.roomName,
        authName: this.authName
      });
    },
    chat4 () {
      this.dialog = true
      this.flag = 'chat4'
      this.flagName = '애니';
      this.roomName = 'chat4';
      this.$socket.emit('req_join_room', {
        roomName: this.roomName,
        authName: this.authName
      });
    },
    sendMessage () {
      //  비속어 필터
      var bad_words = ["존나", "시발", "씨발", "병신"];
      let filteredText;
      const filter = (text) => {
        for(let i = 0; i < text.length; i++){
          for(let j = 0; j < bad_words.length; j++){
            if(text.indexOf(bad_words[j]) != -1) {
              filteredText = text.replace(bad_words[j], "**");
              text = filteredText;
            }
          }
        }
        return text;
      };
      let text = this.message;
      filter(text);
      if(filteredText != null){
        text = filteredText;
      }
      //  입력 내용 전송
      this.$socket.emit('chatMsg',{
          message: text,
          authName: this.authName,
          roomName: this.roomName
      });
      //  내가 전송한 메세지는 [나]로 표시
      this.textarea += "[나] " + text + "\n"
      this.message = ''
    },
    exitRoom () {
      this.$socket.emit('req_exit_room', {
        roomName: this.roomName,
        authName: this.authName
      });
      this.roomName = ''
      this.dialog = false
      //  리렌더링 문제로 강제 새로고침
      this.$router.go();
    }
  }
}
</script>

<style scoped>
.chatroom{
  display: inline-block;
  position: relative;
  margin-right: 130px;
  margin-top: 10px;
  max-height: 45vh;
  width: 35vw;
  /* right: -50%; */
  padding: 0px;
  border-radius: 2.2vh;
  border: 1px solid white;
  background-color: rgba(255, 255, 255, 0.1);
  margin-bottom: 10%;
}
.chatroom button{
  background-color:rgba(18, 193, 236, 0.993); 
  color:white; 
  padding:0.5vw; 
  margin:0.5vw; 
  position: relative;
  right: -50%;
  border-radius: 1vh;
}
.chatroom h4{
  top: 1.3vh;
  font-size: 1.5em;
  left: -2vh;
  color: white;
  position: relative;
}
.icon {
  left: -35px;
}
.ta {
  width: 100%;
  color: whitesmoke;
}
.container{
  background-color:#000C1D;
;
}
.chatroomdiv{
  display: inline-block;
  /* margin-bottom: 50px; */
}
.chatroomdiv h1{
  text-align: start;
  /* width: 300px; */
  /* bottom: -10%; */
}
</style>