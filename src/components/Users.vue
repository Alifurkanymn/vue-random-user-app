<template>
<div class="users">
    <ul v-for="persons in users" :key="persons.results"> 
        <li class="userImg" v-for="persons in users" :key="persons.results"><img :src="persons.picture.large" alt=""></li>
        <li class="subContent">{{subContent}}</li>
        <li>{{text}}</li>
        <img class="icon" src="../assets/images/user.svg" @mouseenter="userName(persons)" />
        <img class="icon" src="../assets/images/mail.svg" @mouseenter="userEmail(persons)" />
        <img class="icon" src="../assets/images/date.svg" @mouseenter="userBirthday(persons)" />
        <img class="icon" src="../assets/images/map.svg" @mouseenter="userAddress(persons)" />
        <img class="icon" src="../assets/images/call.svg" @mouseenter="userPhone(persons)" />
    </ul>
</div>
</template>

<script>
import axios from 'axios'

export default {
    data(){
     return{
        users: [],
        text : "",
        subContent: null,
     }
    },
    mounted () {
    axios
      .get('https://randomuser.me/api/?results=20?inc=name,email,picture,phone')
      .then(response => {
          this.users = response.data.results
      })
  },
  methods:{
    userName(persons){
        this.subContent = "Hi, my name is"
        this.text = persons.name.first + " " + persons.name.last
    },
    userEmail(persons){
        this.subContent = "My email address is"
        this.text = persons.email
    },
    userBirthday(persons){
        this.subContent = "My birthday is"
        this.text = persons.registered.date.slice(0,10)
    },
    userAddress(persons){
        this.subContent = "My address is"
        this.text = persons.location.street.number + " " + persons.location.street.name
    },
    userPhone(persons){
        this.subContent = "My phone number is"
        this.text = persons.phone
    }
  }
}

</script>

<style scoped>
.users{
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color:rgb(235, 252, 235);
}

.subContent{
    font-size:15px;
    color:gray;
}

*{
    list-style: none;
    margin:0;
    padding: 0;
    text-decoration: none;
}
.userImg img{
    border-radius: 100px;
    width: 150px;
    height: 150px;
    transition: 0.3s;
}
.userImg img:hover{
    -ms-transform: scale(1.1); /* IE 9 */
    -webkit-transform: scale(1.1); /* Safari 3-8 */
    transform: scale(1.1); 
    transition: 0.3s;
}
ul{
    border:1px solid rgb(0, 143, 24);
    border-radius: 30px;
    background-color:rgb(250, 250, 250);
    padding: 50px;
    text-align: center;
    padding-right: 80px;
    transition: 0.5s
}
li{
    margin-top:5px;
    font-family:arial,sans-serif;
    font-size:25px;
    transition: 0.5s;
}
.icon{
    margin-top: 30px;
    width:40px;
    height: 40px;
    margin-left:30px;
      transition: 0.3s;

}
.icon:hover{
   -ms-transform: scale(1.1); /* IE 9 */
    -webkit-transform: scale(1.1); /* Safari 3-8 */
    transform: scale(1.1); 
    transition: 0.3s;
}
</style>
