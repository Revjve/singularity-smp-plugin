# Project Singularity

**Project Singularity** is a cyber-simulation survival system designed for **Paper 1.21.8** running on **Java 21**.

The Minecraft world becomes **The Grid**, a digital simulation where players are known as **Units**.  
Each Unit operates using a **Battery (System Uptime)** and a **Neural Chip** that determines their abilities and role within the system.

As time passes, the server progresses through phases that introduce stronger abilities, corruption mechanics, and world events.

---

# Core Systems

## Battery (System Uptime)

Battery represents the **life state of a Unit** and ranges from **0% to 100%**.

If a player's battery reaches **0%**, they become **Corrupted**.

Corrupted players:
- Are placed into **spectator mode**
- Cannot interact with the world
- Must be **revived by another player**

---

## Neural Chip (Class System)

Each player has a **permanent Neural Chip** that determines their abilities.

Each chip contains:
- Passive ability
- Active ability
- Alternate ability

Chips also have **tiers (1–3)** that unlock stronger abilities over time.

---

## Data Storage

Player data is stored using **SQLite**, including:

- UUID
- Battery percentage
- Assigned chip
- Chip tier

---

# Battery States

| Battery | State | Effects |
|------|------|------|
| **80–100%** | Pristine | Normal abilities, name color **AQUA** |
| **20–40%** | Low | Cooldowns doubled, occasional **Nausea / Darkness**, name color **YELLOW** |
| **1–19%** | Critical | Frequent **Darkness flicker**, name color **RED** |
| **0%** | Corrupted | Spectator mode, cannot interact |

---

# Battery Gain

Players can restore battery through several actions:

- **Data Packet** — Right-click to restore battery
- **Corruption Echo** — Interact for **+5% battery**
- **System Repair Kit** — Revives player and restores to **100%**
- **Battery Cell** *(Phase 2+)* — Restores **+5% battery**

---

# Battery Loss

Battery can decrease from:

- **Player death** *(configurable, default 20%)*
- **Phase 3 corruption** *(−1% every 24 hours)*
- **Combat logging** *(battery instantly set to 0%)*

---

# Keybinds

| Key | Action |
|----|----|
| **F** | Use Active Ability *(Tier 2, Phase 2+)* |
| **Shift + F** | Use Alternate Ability *(Tier 3, Phase 3+)* |

---

# Server Phases

## Phase 1 — Boot Sequence (Days 1–7)

- Only **Tier 1 chips**
- **Nether disabled**
- **Repair Kits locked**

---

## Phase 2 — Overclocking (Days 8–21)

- **Tier 2 abilities unlocked**
- **Black Market enabled**
- **Battery Cells available**

---

## Phase 3 — Singularity (Day 22+)

- **Tier 3 alternate abilities unlocked**
- **Corruption begins**
- **Grid Pulse events activated**

---

# Action Bar HUD

Displayed every second:

```
[ UPTIME: XX% | CHIP: CHIP_NAME | TIER: X ]
```

---

# Chip Resonance

If **3 or more players with the same chip** are within **20 blocks**, Resonance activates.

Effects:

- Battery drain **1% per minute shared**
- Passive abilities become **stronger**

---

# Corruption Echoes

If a player dies and reaches **0% battery**, a **ghost echo** appears at their death location.

Interacting with it:

- Provides a **clue**
- Restores **+5% battery**

---

# Grid Pulse Events (Phase 3)

Every **6 hours**, a random global event occurs.

| Event | Effect |
|------|------|
| Firewall Protocol | 20% damage reduction for 10 minutes |
| Memory Leak | Instantly −5% battery |
| Signal Storm | Resets all ability cooldowns |

A warning message is broadcast to chat.

---

# Black Market

Unlocked in **Phase 2**.

Players can trade **battery percentage** for items.

Features include:

- Rare items
- Logic cores
- Neural Scrambler (reroll chip)
- Daily bounty system targeting specific chip types

---

# Glitch Sky

During rain, **falling blocks appear in the sky**.

Features:

- Spawn rate **10× higher during rain**
- Blocks fall **faster than normal**
- Uses most natural overworld blocks except extremely rare ones

Excluded blocks include:

- Diamond ore
- Emerald ore
- Mob spawners

---

# Custom Items & Recipes

### Logic Core
```
D D
  S
D D
```

4 Diamonds + Netherite Scrap

---

### Overclocker (Tier 2 Upgrade)

- 4 Logic Cores
- 1 Beacon

---

### Singularity Core (Tier 3 Upgrade)

- 4 Netherite Ingots
- 1 Beacon

---

### Neural Scrambler

```
R R
  E
R R
```

Redstone + Ender Eye

---

### System Repair Kit

Shapeless:

- Netherite Ingot
- Enchanted Golden Apple

---

### Battery Cell *(Phase 2+)*

Shapeless:

- 1 Diamond
- 4 Iron Ingots

---

# Item Effects

| Item | Effect |
|------|------|
| Data Packet | Restores battery |
| Neural Scrambler | Rerolls chip (50% chance −10% battery) |
| Overclocker | Upgrade Tier 1 → Tier 2 |
| Singularity Core | Upgrade Tier 2 → Tier 3 |
| Repair Kit | Revive corrupted player |
| Battery Cell | Restore +5% battery |

---

# Custom Model Data

| Item | Model ID |
|------|------|
| Corrupted Data Packet | 1001 |
| Degraded Data Packet | 1002 |
| Encrypted Data Packet | 1003 |
| Pristine Data Packet | 1004 |
| Logic Core | 2001 |
| Overclocker | 2002 |
| Singularity Core | 2003 |
| Neural Scrambler | 2004 |
| System Repair Kit | 2005 |
| Battery Cell | 2006 |

---

# Commands

## Player Commands

```
/singularity help
/singularity info
/singularity phase
/blackmarket
```

---

## Admin Commands

```
/singularity admin battery <player>
/singularity admin setbattery <player> <amount>
/singularity admin chip <player>
/singularity admin setchip <player> <chip>
/singularity admin revive <player>
/singularity admin setphase <phase>
/singularity admin giveitem <player> <item> [amount]
```

---

# Important Notes

- Abilities require the **correct phase and tier**
- **Low battery doubles cooldowns**
- In **Phase 3**, Tier 3 players receive **25% reduced ability cooldowns**
