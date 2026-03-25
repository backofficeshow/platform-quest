# Platform Quest

A 10-level platformer game built with vanilla JavaScript and HTML5 Canvas.

Try it here: https://platform-quest.andrew-ce0.workers.dev/

## Game Overview

- **Objective**: Complete all 10 levels by defeating all enemies (and bosses) to unlock the exit, then collect the treasure to advance
- **Controls**:
  - `WASD` or `Arrow Keys` - Move and jump
  - `Space` - Jump
  - `Z` or `K` - Attack (requires sword)
  - `X` or `J` - Throw torch (requires torch ammo)
  - `Shift` - Dash (requires dash power-up)
  - `R` - Restart (on game over or win)
  - `Enter` - Continue (if save exists)
  - `Space`, `Z`, or Click - Start game from title screen
  - Mouse - Click buttons on title screen

## Game Mechanics

### Player
- Starts each level with 3 health (max 5 with heart pickups)
- Can move left/right and jump
- Attacking with sword creates a hitbox in front of player
- Invincible briefly after taking damage (flashing effect)
- Can acquire power-ups: double jump and dash

### Power-ups
- **Double Jump** (green orb with ^): Press jump again while in the air to jump higher
- **Dash** (magenta icon): Hold Shift to dash in facing direction
- Power-ups persist between levels

### Sword
- **Not available from start** - must be collected in each level
- Located at a specific position in each level
- Required to damage enemies with attack (Z/K keys)
- Visual: Silver blade with brown handle, golden glow
- **Sound**: Metallic "shing" when collected (Zelda-style)

### Torches
- **3 torches per level** - scattered across the level
- Pick up by walking over them
- Throw with `X` or `J` keys
- Arc trajectory with gravity
- **Instantly kills** any enemy on contact
- Explodes with orange particles when hitting enemy or ground

### Hearts
- **1 heart per level** - restores 1 health when collected
- Only works if player health is below max (5)
- Visual: Red heart shape

### Gems
- **2 gems per level** - placed in hard-to-reach locations
- Collect for +50 bonus points
- Visual: Cyan diamond shape with bobbing animation

### Secret Rooms
- Hidden areas (red-tinted) in select levels
- Walk into the tinted area to discover it
- Contains bonus platforms and gems inside
- Adds exploration incentive

### Enemies

**Red Enemies**
- 2 HP, faster movement
- Patrol platforms back and forth

**Blue Enemies**
- 3 HP, slower movement
- Same patrol behavior

**Purple Shooters**
- 2 HP, stationary
- Shoot magenta projectiles at the player every ~2 seconds
- Projectiles deal 1 damage on contact
- Appear in later levels (7-10)

**Boss (Levels 5 & 10)**
- 20 HP, large enemy
- Phase 2 at 50% health (harder attack patterns)
- Shoots multiple projectiles in patterns
- Must defeat to unlock treasure
- Awards +500 points

**Behavior**
- Move along platforms (except purple/boss)
- Reverse direction at platform edges
- Damage player on contact (1 HP)
- Knockback when hit by sword
- Flash white when hit (hitTimer)
- Drop score and particles on death

### Exit/Treasure
- **Locked** (gray) until all enemies defeated (and boss on levels 5/10)
- **Unlocked** (gold) when enemies remaining = 0
- Collecting treasure advances to next level
- Game auto-saves progress when collecting treasure
- Level 10 treasure triggers win screen

### Levels

The game has 10 levels with increasing difficulty:

1. **Level 1**: 3 enemies, 1 moving platform, double jump power-up
2. **Level 2**: 4 enemies, 1 moving platform
3. **Level 3**: 3 enemies, 1 moving platform, dash power-up
4. **Level 4**: 4 enemies, 1 moving platform
5. **Level 5**: 4 enemies, 1 moving platform, **BOSS BATTLE**
6. **Level 6**: 5 enemies, 1 moving platform, 1 purple shooter
7. **Level 7**: 4 enemies, 2 moving platforms (opposing), 1 purple shooter
8. **Level 8**: 5 enemies, 1 moving platform, 1 purple shooter
9. **Level 9**: 6 enemies, 1 moving platform, 1 purple shooter
10. **Level 10**: 6 enemies, 2 moving platforms (opposing), **FINAL BOSS**

Each level contains:
- Unique platform layout
- Specific enemy positions
- 1 sword pickup
- 3 torch pickups
- 1 heart pickup
- 2 gems
- 1 treasure/exit
- Secret room (levels 1-4)
- Power-ups in select levels

### Scoring
- Enemy kill: +100 points
- Torch kill: +150 points
- Gem collected: +50 points
- Boss defeated: +500 points
- Level completion: No bonus (score accumulates)

### Sound Effects (Web Audio API)
- `jump` - Player jumps
- `attack` - Sword swing
- `sword` - Pick up sword (metallic Zelda-style chime)
- `hit` - Enemy hit by sword
- `enemyDeath` - Enemy dies
- `treasure` - Collect item
- `hurt` - Player takes damage
- `win` - Complete all levels

### Save/Load
- Game auto-saves to localStorage when collecting treasure
- Title screen shows "CONTINUE" button if save exists
- Press Enter to continue from last level
- Press Space/Z or click "NEW GAME" to start fresh
- Save is cleared when restarting after win/game over (R key)

## How to Run

Simply open `index.html` in a modern web browser. The game runs on a local HTTP server on port 3000:

```bash
python3 -m http.server 3000
```

Then visit http://localhost:3000
