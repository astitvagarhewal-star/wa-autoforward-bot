# Termux WA-Bot 🚀  
[![GitHub last commit](https://img.shields.io/github/last-commit/jaival-11/wa-autoforward-bot?style=for-the-badge&color=blue)](https://github.com/jaival-11/wa-autoforward-bot/commits/main)


A headless WhatsApp auto forwarding bot designed to run natively on Android via Termux. Features a Web UI for easy configuration and a Telegram logging system for network monitoring, critical alerts and status updates
  
## ✨ Features
(This may not be a complete list, I am adding existing features to list with commits)

* **🌐 Web UI:** A beautiful, lightweight Express.js dashboard to monitor and configure bot's settings locally on your device.  
* **📷 QR code login:** On first time launching the bot, Web UI will show a WhatsApp Web QR code which you need to scan to authorise the bot as a linked device, and perform actions. You can always log out from Web UI, and log in with another account whenever you wish.  
* **⏩️ Native forwarding:** Uses WhatsApp's native forwarding to ensure every kind of message is forwarded to the target chat.  
* **🛡 Strict whitelist compliance:** The bot forwards messages only of whitelisted users, configured using the Web UI, non-whitelisted users are treated silently and a log is sent via Telegram bot.  
* **📝 Telegram Logging:** Sends notifications via Telegram bot for every bot status updates. The logs include meaningful hashtags for easy searching.  
* **⏳️ Smart Rate Limiting:** Implements mathematically calculated delays to prevent server-side rate limiting.  
* **☁️ Media/messages back-up:** Every forwarded message generates a Telegram log containing the respective media files and text.  
* **🚦Queue system:** Advanced queue management ensure that messages sent within short period of time are held back and processed sequentially to ensure stability, and preventing rate limiting.  
* **📶 Network Outage reporting:** Watchdog watches for internet connection every 30s, and if internet connection is not detected, it sends a push notification using [Termux:API](https://github.com/termux/termux-api) and suspends the heartbeat. When internet connection is restored, watchdog dismisses the push notification and sends telegram log with downtime and timestamps.  
* **🩺 Heartbeat:** Termux console prints heartbeat every 10 mins so you know your bot never slept. There is a toggle in Web UI to enable/disable sending heartbeat via telegram bot.
* **🔑 Passphrase Auto-Whitelisting:** Allows users to secretly authorize themselves by sending a specific `/id [passphrase]` command, automatically updating the whitelist without admin intervention. Once authorised, their messages will continue to forward until removed from whitelist. Telegram bot sends log whenever a new user authorises using the command. Passphrase and passphrase toggle can be configured in Web UI.
* **🔍 Silent ID Retrieval:** User can send `/id` command on WhatsApp, and Telegram bot will pass the id information in the log. 
* **👻 Ghost Packet & Duplicate filtering:** Intercepts and drops malformed network packets or duplicate event triggers before they can crash the queue, ensuring continued operations.  
* **🩹 Error recovery:** Automatically handles deleted messages and network errors, ensuring continuous operation without freezing.    
* **🧹 Automated memory optimisation:** Flushes network deduplication cache every hour to keep the script lightweight.  
* **​📱 Termux & Android Optimized:** Specifically architected to run 24/7 on Android devices.  
   
`and many more....`
 
## 🖼 Web UI Screenshot
![Screenshot_20260413_203116_DuckDuckGo(1)](https://github.com/user-attachments/assets/386bdb70-eb7b-40fe-81b5-7f15ca4f4a84)


## 📋 Prerequisites
>**⚠️ Note:** Read [Disclaimer](https://github.com/jaival-11/wa-autoforward-bot?tab=readme-ov-file#%EF%B8%8F-legal-disclaimer--tos-warning) before proceeding with installation and use.  


Before installing, ensure you have the following ready:
* **Android Device:** With [Termux](https://termux.dev/) and [Termux:API](https://github.com/termux/termux-api) installed with necessary permissions granted.
* **Node.js, Git, Chromium:** Installed within Termux environment.  
  ```
  pkg install nodejs git chromium -y
  
  ```
* **Telegram Bot:** A bot token from [@BotFather](https://t.me/BotFather) and your personal/channel Telegram Chat ID for logs.
* **WhatsApp Accounts:** One account to run the bot, and the target chat/group where messages will be forwarded.

## 🚀 Installation (Termux)
Copy and paste the below code block into your termux session:
```
# 1. Clone the repository
git clone https://github.com/jaival-11/wa-autoforward-bot.git

# 2. Navigate to the folder
cd wa-autoforward-bot

# 3. Install the dependencies
npm install

# 4. Copy the example config
cp config.example.json config.json

# 5. Acquire wakelock
termux-wake-lock

# 6. Set up alias
echo "alias wa-bot-jaival='cd ~/wa-autoforward-bot && termux-wake-lock && node bot.js'" >> ~/.bashrc

# 7. Start the bot
node bot.js

```
8. Launch Web UI at `http://localhost:3000` and configure the bot.

## 💻 Usage & Web UI
Once the bot is running, you don't need to touch the code to manage it. 
1. Open your device's browser and go to `http://localhost:3000`
2. Use the **🌐 Web UI** to easily update the bot parameters, and monitor bot status
3. Keep Termux running in the background (wakelock acquired), and the bot will handle the rest!

**👉 To stop the bot, and exit termux session safely:**  
Press `Ctrl+C`, and then exit termux by clicking `Release wakelock` and `Exit` on Termux notification.  

**👉 To launch the bot:**  
To launch the bot, you don't need to do  [Installation](https://github.com/jaival-11/wa-autoforward-bot?tab=readme-ov-file#-installation-termux) again. You need to open termux, and type ``` wa-bot-jaival ``` in home directory (after ` ~ $ `)that's it now wait for few seconds and your bot will start. You will also receive confirmation via Telegram
  
**👉 To update the bot to match latest commit:**

Stop the bot (Ctrl+C), copy and paste below code block in termux session:
```
# 1.
git pull origin main

# 2. Update dependencies
npm install

# 3. Restart the bot
node bot.js

```
## 🐛 Bugs & Feature Requests
Have an idea to make this bot better? Found a bug? Have any question? Feel free to open an issue in this repository! Contributions and feature requests are always welcome. You can also reach out to me directly (details at end)

## 📚 Tech Stack (for nerds):

**Core Environment & Language** ![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Termux](https://img.shields.io/badge/Termux-000000?style=for-the-badge&logo=termux&logoColor=white)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)

**Backend & Automation** ![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![Puppeteer](https://img.shields.io/badge/puppeteer-%2340B5A4.svg?style=for-the-badge&logo=puppeteer&logoColor=white)
![Axios](https://img.shields.io/badge/axios-671ddf?&style=for-the-badge&logo=axios&logoColor=white)

**Web UI** ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)

**APIs & Integrations** ![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram_Bot_API-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)


## ⚠️ LEGAL DISCLAIMER & TOS WARNING
**USE AT YOUR OWN RISK.** This project is for educational and research purposes only. Running automated bots on WhatsApp is a violation of WhatsApp's Terms of Service. Using this software may result in your WhatsApp number being permanently banned. The creator of this software (Jaival) is NOT responsible for any account bans, data loss, or legal repercussions caused by using this code. Always ensure you have the recipient's consent before automated forwarding. This project is not affiliated, associated, authorized, endorsed by, or in any way officially connected with WhatsApp or any of its subsidiaries or its affiliates. All product names, logos, brands, and other trademarks featured or referred to within this project are the property of their respective trademark holders. These trademark holders are not affiliated with this project or its developers.
  
>**💡 Developer Note:** This project was created to explore the technical side of message forwarding. If you're looking to stay in WhatsApp's good graces, I highly recommend checking out their official Business API instead!


## 🙏 Acknowledgments & Credits
This project would not be possible without the incredible work of the open-source community. Major credits to:

* **[whatsapp-web.js](https://wwebjs.dev/):** The core library powering the WhatsApp web client integration.
* **[Puppeteer](https://pptr.dev/):** For handling the headless Chromium browser.
* **[Express.js](https://expressjs.com/):** For powering the local web dashboard.
* **[Termux](https://termux.dev/):** The ultimate Android terminal emulator environment.
* **[Termux:API](https://wiki.termux.com/wiki/Termux:API):** For triggering native Android push notifications during network outages.
* **[Axios](https://axios-http.com/) & [form-data](https://www.npmjs.com/package/form-data):** For managing the HTTP requests and media payloads sent to Telegram.
* **[qrcode-terminal](https://www.npmjs.com/package/qrcode-terminal) & [qrcode.js](https://davidshimjs.github.io/qrcodejs/):** For handling QR code generation in both the CLI and the Web UI.
* **[Telegram Bot API](https://core.telegram.org/bots/api):** For providing the infrastructure that handles remote network logging and heartbeats.


## 🤖 AI Disclaimer
This project— including the codebase, documentation (README and LICENSE files)—was developed with the assistance of AI. (P.s. I am new to this, apologies!)

## 📜 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for more information.

## 🤝 Attribution & Support:

This project is open-source and made available under the [MIT License](LICENSE), but I would deeply appreciate visible credit or a link back to this repository in your project or application if you choose to implement it. A little attribution goes a long way!

⭐️ **Support the Project:**
If you like `wa-autoforward-bot` and found it useful for your workflow, please consider giving this repository a star! It helps others discover the project and motivates further development.

---
[![Creator Badge](https://img.shields.io/badge/%F0%9F%8C%90%20Created%20by%20-%20Jaival%20-%20blue?style=for-the-badge&labelColor=&color=blue)](https://github.com/jaival-11)  


[![X (formerly Twitter) Follow](https://img.shields.io/twitter/follow/techironic11?style=for-the-badge&logo=X&labelColor=blue&color=orange)](https://x.com/techironic11)

[![Email](https://img.shields.io/badge/Email-jaival7909%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white&color=blue)](mailto:jaival7909@gmail.com)


