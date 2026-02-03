# CYBER ARENA - Code Guide 🚀

Welcome! This guide will help you understand how the game is organized and how to make changes.

## 📁 File Structure

The game is now split into **6 simple files** instead of one giant file. This makes it easier to find and change things!

```
spaceshooter/
├── index.html              # Main HTML file (loads everything)
├── styles/
│   └── main.css           # Game styling (colors, layout)
└── src/
    ├── config.js          # Game settings and data
    ├── utils.js           # Helper functions
    ├── systems.js         # Save/load and achievements
    ├── scenes.js          # All game screens
    └── main.js            # Starts the game
```

## 🎮 What Each File Does

### 📄 `index.html`
- The main page that loads the game
- Links to the CSS file
- Loads all JavaScript files in the right order
- **You rarely need to change this file!**

### 🎨 `styles/main.css`
- Controls how the game looks on the page
- Sets the black background
- Centers the game on screen
- **Change this if you want different page styling**

### ⚙️ `src/config.js` - Game Settings
This is where you change game balance and settings!

**What's inside:**
- `W` and `H` - Canvas width and height
- `SHIPS` array - All three ships and their stats
  - Change `baseHp`, `baseSpeed`, `baseDmg` to make ships stronger/weaker
  - Modify ship colors and descriptions
- `ACHIEVEMENTS` - All unlockable achievements
- `PERSISTENT_UPGRADES` - Permanent upgrades between games

**Example: Make VIPER ship faster**
```javascript
{
  name: 'VIPER',
  baseSpeed: 300,  // Changed from 240 to 300!
  // ... other properties
}
```

### 🔧 `src/utils.js` - Helper Functions
This file has useful tools that the game uses.

**What's inside:**
- **Math functions**: `clamp()`, `rand()`, `dist()`, `norm()`
- **Drawing functions**: `drawShipPreview()`, `drawShipInGame()`
  - These draw the cool ship graphics!
  - You can edit these to change how ships look
- **Audio system**: `initAudio()`, `beep()`, `sfx()`
  - All the sound effects

**Tip:** If you want to add a new sound effect, add it to the `sfx()` function!

### 💾 `src/systems.js` - Saving & Achievements
Handles saving your progress and unlocking achievements.

**What's inside:**
- `loadPersistent()` - Loads saved data when you start the game
- `savePersistent()` - Saves your progress
- `unlockAchievement()` - Awards achievements
- `trackEnemyKill()` - Counts your total kills

**Don't change this file unless you know what you're doing!**

### 🎬 `src/scenes.js` - All Game Screens
This is the **BIGGEST** file! It contains all four game screens (scenes):

1. **MenuScene** - Main menu with ship selection
2. **AchievementsScene** - View your achievements
3. **GameScene** - The actual game (where you play!)
4. **GameOverScene** - Shows your score when you die

**Most of the game logic is in `GameScene`**:
- `create()` - Sets up the game when it starts
- `update()` - Runs every frame (handles movement, shooting, enemies)
- `draw()` - Draws everything on screen
- Enemy update functions - How each enemy type behaves
- `fire()` - Weapon firing logic
- `nextWave()` - Spawns new waves of enemies

**Example: Make enemies spawn faster**
Look for `nextWave()` in GameScene and change the spawn timing!

### 🎯 `src/main.js` - Game Starter
The smallest file! Just starts the game.

**What it does:**
- Creates the Phaser game configuration
- Tells Phaser which scenes to use
- Starts everything running

**You rarely need to change this!**

## 🛠️ Common Changes You Might Want to Make

### Change Ship Stats
**File:** `src/config.js`
Look for the `SHIPS` array and modify:
- `baseHp` - Health points
- `baseSpeed` - Movement speed
- `baseDmg` - Damage per shot
- `baseRate` - Fire rate (lower = faster)

### Add a New Achievement
**File:** `src/config.js`
Add to the `ACHIEVEMENTS` object:
```javascript
myNewAchievement: {
  name: 'My Achievement',
  desc: 'Do something cool!',
  unlocked: false
}
```

Then trigger it in `src/scenes.js` by calling:
```javascript
unlockAchievement('myNewAchievement');
```

### Modify Enemy Behavior
**File:** `src/scenes.js`
Find the `GameScene` class and look for enemy update functions like:
- `updateHealer()`
- `updateBomber()`
- `updateKamikaze()`

Change the movement, shooting, or special abilities!

### Change Colors
**File:** `src/config.js`
Ship colors are in hex format like `0x00ffff` (cyan)
- `0x00ffff` = Cyan (light blue)
- `0x7733ff` = Purple
- `0xff6600` = Orange
- `0xff0000` = Red
- `0x00ff00` = Green

### Add New Sound Effects
**File:** `src/utils.js`
Add a new case to the `sfx()` function:
```javascript
case 'mySound':
  beep(440, 'sine', 0.1, 0.2);  // frequency, type, volume, duration
  break;
```

Then call it with: `sfx('mySound')`

## 🐛 Debugging Tips

### Game won't load?
1. Open browser console (F12)
2. Look for error messages in red
3. Check that all file paths in `index.html` are correct

### Changed something but nothing happened?
1. Hard refresh the page (Ctrl+F5 or Cmd+Shift+R)
2. Clear browser cache
3. Check console for errors

### Want to see what's happening?
Add `console.log()` statements in the code:
```javascript
console.log('Player HP:', this.p.hp);
console.log('Current wave:', this.wave);
```

## 📚 Learning Resources

- **Phaser Documentation**: https://photonstorm.github.io/phaser3-docs/
- **JavaScript Tutorial**: https://javascript.info/
- **Game Dev for Kids**: https://www.khanacademy.org/computing/computer-programming

## 🎉 Have Fun!

Remember: The best way to learn is by experimenting!
- Try changing numbers
- See what breaks
- Figure out how to fix it
- Repeat!

Don't be afraid to make mistakes - you can always undo changes with Git!

Happy coding! 🚀👾
