# Donbot

![GitHub](https://github.com/bearstronk/donbot)
![Discord.js](https://img.shields.io/badge/Discord.js-14.16.2-blue)
![Node.js](https://img.shields.io/badge/Node.js-16.0.0-green)

**Donbot** is a feature-rich Discord bot that brings the a long form Mafia bot to your server, based on a mix of standard Mafia and Town of Salem ruleset!

---

## 📖 Table of Contents

- [Features](#features)
- [Installation](#installation)
  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Commands](#commands)
  - [Gameplay](#gameplay)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎉 Features

- **Role Assignment:** Automatically assigns roles such as Mafia, Doctor, Detective, Bodyguard, Mayor, and President.
- **Private Mafia Chat:** Mafias have their own private thread to discuss strategies.
- **Interactive Phases:** Engaging button-based interactions for joining/leaving games, voting, and using special abilities.
- **Multiple Abilities:** Roles like Doctor, Detective, Bodyguard, Mayor, and President have unique abilities to influence the game.
- **Win Condition Checks:** Automatically determines when the game has been won by either the Mafia or the Citizens.
- **Robust Error Handling:** Ensures smooth gameplay with comprehensive error management.

## 🛠 Installation

### Prerequisites

- **Node.js:** Ensure you have Node.js v16.0.0 or higher installed. [Download Node.js](https://nodejs.org/)
- **Discord Account:** A Discord account to manage and invite the bot to your server.
- **Discord Server:** Admin access to a Discord server where you can add the bot.

### Setup

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/bearstronk/donbot.git
   ```

2. **Install Dependencies:**

   ```bash
   npm install
   ```

3. **Create a Discord Bot:**

   - Go to the [Discord Developer Portal](https://discord.com/developers/applications).
   - Click on **"New Application"** and name it (e.g., Donbot) 
   - Navigate to the **"Bot"** section and click **"Add Bot"**.
   - Copy the **Bot Token**. **Keep it secure!**

4. **Configure the Bot:**

   - Create a `config.js` file in the root directory:

     ```javascript
     module.exports = {
      
         token: 'YOUR_DISCORD_BOT_TOKEN',
         allowedRoleId: 'ROLE_ID_ALLOWED_TO_START_GAME',
         startTime: 30000, // Time in milliseconds before the game starts after initiation
         maxPlayers: 20, // Maximum number of players allowed in a game
         minPlayers: 6, // Minimum number of players required to start a game
         mafiaKillTime: 60000, // Time allocated for Mafia to choose a kill
         docActionTime: 60000, // Time allocated for Doctor to protect
         bodyguardPhaseTime: 60000, // Time allocated for Bodyguard phase
         detectorPhaseTime: 60000, // Time allocated for Detective phase
         citizenVoteTime: 60000, // Time allocated for Citizens to vote
     };
     ```

     - **Parameters:**
       - `token`: Your Discord bot token.
       - `allowedRoleId`: The role ID that is permitted to start the game (e.g., `-مافيا` command).
       - `startTime`: Countdown time before the game starts.
       - `maxPlayers`: Maximum players in a single game.
       - `minPlayers`: Minimum players required to start the game.
       - `mafiaKillTime`, `docActionTime`, `bodyguardPhaseTime`, `detectorPhaseTime`, `citizenVoteTime`: Time allocations for various phases in milliseconds.

5. **Invite the Bot to Your Server:**

   - Navigate to the **"OAuth2"** section in the Discord Developer Portal.
   - Click on **"URL Generator"**.
   - Under **"Scopes"**, select `bot`.
   - Under **"Bot Permissions"**, select the following:
     - `Send Messages`
     - `Manage Messages`
     - `Read Message History`
     - `Manage Threads`
     - `Use External Emojis`
     - `Connect` (if voice features are added in the future)
   - Copy the generated URL and open it in your browser.
   - Select the server you want to add the bot to and authorize.

6. **Start the Bot:**

   ```bash
   npm start
   ```

   You should see console logs indicating the bot is online:

   ```
   Logged in as YourBotName#1234
   Code by Bearstrong
   discord.gg/
   ```

---

## ⚙ Configuration

Ensure your `config.js` is correctly set up with all necessary parameters. Here's a sample configuration:

```javascript
module.exports = {
    token: 'YOUR_DISCORD_BOT_TOKEN',
    allowedRoleId: 'ROLE_ID_ALLOWED_TO_START_GAME',
    startTime: 86400000, 
    mafiaKillTime: 2147483647, 
    docActionTime: 2147483647, 
    detectorPhaseTime: 2147483647, 
    citizenVoteTime: 2147483647, 
    bodyguardPhaseTime: 2147483647, 
    maxPlayers: 20, 
};
```

**Notes:**

- Replace `'YOUR_DISCORD_BOT_TOKEN'` with your actual bot token.
- Replace `'ROLE_ID_ALLOWED_TO_START_GAME'` with the ID of the role that should have permission to start the Mafia game (typically a moderator or admin role).

---

## 🚀 Usage

### 📜 Commands

- **Start Game:**

  - **Command:** `-mafia`
  - **Description:** Initiates the Mafia game. Only users with the specified role (`allowedRoleId`) can use this command.
  - **Example:**
    ```
    -مافيا
    ```

### 🎮 Gameplay

1. **Starting the Game:**

   - A user with the allowed role sends the `-mafia` command.
   - The bot sends an embed with buttons to **Join** or **Leave** the game.
   - Players click **Join** to participate.
   - After the countdown (`startTime`), the game begins if the minimum number of players is met.

2. **Role Assignment:**

   - Roles are randomly assigned:
     - **Mafia:** Based on player total 1 Mafia per four players up to 4 total  mafia.
     - **Doctor, Detective, Bodyguard, Mayor, President, Clown:** 1 player each.
     - **Citizens:** Remaining players.
   - Mafia members get a private thread to discuss.

3. **Night Phases:**

   - **Mafia Phase:** Mafia members choose a player to kill.
   - **Doctor Phase:** Doctor chooses a player to protect.
   - **Bodyguard Phase:** Bodyguard can shield a player from being killed.
   - **Detective Phase:** Detective can investigate a player's role.

4. **Day Phases:**

   - Players discuss and vote to eliminate suspected Mafia members.
   - Special roles like **President** and **Mayor** can influence voting.

5. **Win Conditions:**

   - **Citizens Win:** All Mafia members are eliminated.
   - **Mafia Wins:** Mafia members equal or outnumber citizens.

6. **Independent Win Conditons**
  - **Clown:** The clown instead has to win by tricking the town into voting for them during the day phase. If the clown lives until the end of the game the clown loses. If the clown is killed by the Mafia, the clown loses.  THE CLOWN WINNING OR LOSING DOES NOT EFFECT THE LARGER GAME AT HAND

### 📌 Special Abilities

- **President:**
  - Can override a day phase vote with a Veto and choose who is voted out.
- **Mayor:**
  - Has a day phase voting power of two votes.
- **Detective:**
  - Can reveal a player's role once per game.
- **Doctor:**
  - Can protect a player from being killed once per game.
- **Bodyguard:**
  - Can shield a player from being killed once per game.
- **Clown:**
  - An agent of chaos whose goal is to get killed and sow dissent. 

### 🛠️ Buttons and Interactions

- **Join/Leave Game:**
  - Players use buttons to join or leave the game lobby.
- **Voting:**
  - Players vote using buttons to eliminate a suspected Mafia member.
- **Special Abilities:**
    **President**:On clicking the Veto button the player can choose any individual to remove from the game.
    **Detective**: On clicking the Detect button the player can choose any individual and reveal their role.


---

## 🤝 Contributing

We welcome contributions from the community! To contribute:

1. **Fork the Repository**

2. **Create a Feature Branch:**

   ```bash
   git checkout -b feature/YourFeature
   ```

3. **Commit Your Changes:**

   ```bash
   git commit -m "Add some feature"
   ```

4. **Push to the Branch:**

   ```bash
   git push origin feature/YourFeature
   ```

5. **Open a Pull Request**

Please ensure your code follows the existing style and includes appropriate documentation.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 📫 Contact

- **Author:** Bearstrong
- **GitHub:** [Donbot](https://github.com/bearstronk/donbot)
- **Discord:** bearstrong


---

## 💡 Future Enhancements

- **Additional Roles:** Introduce more unique roles to diversify gameplay.
- **Customization:** Allow server admins to customize roles and game settings.

---

Thank you for checking out this longform Mafia Discord Bot!
