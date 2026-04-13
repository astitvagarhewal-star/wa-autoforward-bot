# Termux WA-Bot 🚀

A highly resilient, headless WhatsApp bot designed to run natively on Android via Termux. Features a Web UI and a Telegram logging system for network monitoring, critical alerts and status updates
  
## ✨ Features
(This is not a complete list, I am adding existing features to list with each commit)

**🌐 Web UI:** A beautiful, lightweight Express.js dashboard to monitor and configure bot's settings locally on your device. <br>
**📷 Qr code login:** On first time launching the bot, it will show you a WhatsApp Web qr code which you need to scan to authorise the bot as a linked device, and perform actions. You can always log out from Web UI, and log in with another account whenever you wish <br>
**⏩️ Native forwarding:** Uses WhatsApp's native forwarding to ensure every kind of message is forwarded to the target chat. <br>
**🛡 Strict whitelist compliance:** The bot forwards messages only of whitelisted users, configured using the Web UI, non whitelisted users are treated silently and log is sent on telegram. <br>
**📝 Telegram Logging:** Sends notifications via Telegram bot for every bot status updates. The logs have meaningful hashtags used so you can easily search them<br>
**✍️ Human Behavior simulation:** Tries to escape bot behavior detection by using mathematically calculated delays for reading, typing and 'online presence'. <br>
**☁️ Media/messages back-up:** Every message forwarded creates a log in telegram which includes media file forwarded. <br>
**🚦Queue system:** Advanced asynchronous lock-and-release mechanics ensure that messages sent within short period of time are held back and processed sequentially trying not to trigger race conditions or server bans. <br>
**📶 Network Outage reporting:** Watchdog watches for internet connect every 30s, and if internet connection is not detected it sends a push notification using [Termux:API](https://github.com/termux/termux-api) and suspends heartbeat. When internet connection is restored, watchdog dismisses the push notification and sends telegram log with downtime and timestamps. <br>
**🩺 Heartbeat:** Termux console prints heartbeat every 10 mins so you know your bot never slept. There is a toggle in Web UI to enable/disable sending heartbeat via telegram bot. <br>
​**🔑 Passphrase Auto-Whitelisting:** Allows trusted users to secretly authorize themselves by sending a specific /id [passphrase] command, automatically updating the whitelist without admin intervention. Passphrase and passphrase toggle can be configured in Web UI. <br>
​**🔍 Silent ID Retrieval:** User can send /id command on WhatsApp, and Telegram bot will pass the id information. <br>
**👻 Ghost Packet & Duplicate filtering:** Intercepts and drops malformed network packets or duplicate event triggers before they can crash the queue. <br>
**🩹 Error recovery:** Automatically skips deleted messages, or errors occured, doesn't get stuck and continues the operations. <br>
**🧹 Automated memory optimisation:** Flushes network deduplication cache every hour to keep the script lightweight. <br>
**​📱 Termux & Android Optimized:** Specifically architected to run 24/7 on Android devices using headless Chromium, perfectly bridging mobile hardware with backend automation. <br>
<br>`and many more....`
 
## 🖼 Web UI Screenshot
<a href="https://github-production-user-asset-6210df.s3.amazonaws.com/251092232/577435433-9d45efff-5484-43d3-a084-ecc313618911.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260413T151753Z&X-Amz-Expires=300&X-Amz-Signature=4c0ccc9c452b3c8186c992c9e4dc091f6e7f68a424a83b0c127db04687dc3243&X-Amz-SignedHeaders=host&response-content-type=image%2Fjpeg">
  <img src="https://github-production-user-asset-6210df.s3.amazonaws.com/251092232/577435433-9d45efff-5484-43d3-a084-ecc313618911.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20260413%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260413T151753Z&X-Amz-Expires=300&X-Amz-Signature=4c0ccc9c452b3c8186c992c9e4dc091f6e7f68a424a83b0c127db04687dc3243&X-Amz-SignedHeaders=host&response-content-type=image%2Fjpeg" width="200" alt="Thumbnail Description">
</a>

## 📋 Prerequisites
Before installing, ensure you have the following ready:
* **Android Device:** With [Termux](https://termux.dev/) and [Termux:API](https://github.com/termux/termux-api) installed with necessary permissions granted.
* **Node.js:** Installed within your Termux environment (`pkg install nodejs`).
* **Telegram Bot:** A bot token from [@BotFather](https://t.me/BotFather) and your personal/channel Telegram Chat ID for logs.
* **WhatsApp Accounts:** One account to run the bot, and the target chat/group where messages will be forwarded.

## 🚀 Installation (Termux)
1. Clone this repository: `git clone https://github.com/jaival-11/wa-autoforward-bot.git`
2. Navigate to the folder: `cd wa-autoforward-bot`
3. Install dependencies: `npm install`
4. Copy the example config: `cp config.example.json config.json`
5. Start the bot: `node bot.js`
6. Launch Web UI at `http://localhost:3000` and configure the bot.

## 💻 Usage & Web UI
Once the bot is running, you don't need to touch the code to manage it. 
1. Open your device's browser and go to `http://localhost:3000`
2. Use the **🌐 Web UI** to easily update the bot parameters, and monitor bot status
3. Keep Termux running in the background (wakelock acquired), and the bot will handle the rest!

## ⚠️ LEGAL DISCLAIMER & TOS WARNING
**USE AT YOUR OWN RISK.** This project is for educational and personal use only. Running automated bots on WhatsApp is a violation of WhatsApp's Terms of Service. Using this software may result in your WhatsApp number being permanently banned. The creator of this software (Jaival) is NOT responsible for any account bans, data loss, or legal repercussions caused by using this code. Always ensure you have the recipient's consent before automated forwarding.

## 🐛 Bugs & Feature Requests
Have an idea to make this bot better? Found a bug? Feel free to open an issue in this repository! Contributions and feature requests are always welcome.

## 🙏 Acknowledgments & Credits
This project would not be possible without the incredible work of the open-source community. Major credits to:
* **[whatsapp-web.js](https://github.com/pedroslopez/whatsapp-web.js):** The core library powering the WhatsApp web client integration.
* **[Puppeteer](https://github.com/puppeteer/puppeteer):** For handling the headless Chromium browser.
* **[Express.js](https://expressjs.com/):** For powering the local web dashboard.
* **[Termux](https://termux.dev/):** The ultimate Android terminal emulator environment.
* **[Termux:API](https://github.com/termux/termux-api):** Send push notifications for network outage

## 🤖 AI Disclaimer
This project—including the codebase, all documentation (README and LICENSE files)—was developed with the assistance of AI. (I am new to this, apologies!)

## 📜 License
Distributed under the MIT License. See `LICENSE` for more information.

---
**Created by Jaival** 🌐 [Follow me on X (Twitter)](https://x.com/techironic11)
