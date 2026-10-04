# ROS New Player's Guide

*A levelling guide for **ROS (Realms of Simulacra)**, a MUD derived from RoT 2.0 and ROM 2.4. It assumes you have played graphical MMOs but never a MUD.*

**To play:** connect to **`ros.simlives.net`**, port **`4000`**, with a MUD client such as [Mudlet](https://www.mudlet.org/), or with plain telnet (`telnet ros.simlives.net 4000`). Type a new name at the login prompt to create a character.

Everything below was taken from this server's own source code and area files, and checked by playing on a test copy of the game. Where the in-game `help` files disagree with how the game actually behaves, this guide follows the actual behaviour and says so.

---

## Contents

1. [MUDs for MMO players](#1-muds-for-mmo-players)
2. [Reading this guide](#2-reading-this-guide)
3. [Character creation, step by step](#3-character-creation-step-by-step)
4. [Your first hour: gearing up and the Mud School](#4-your-first-hour-gearing-up-and-the-mud-school)
5. [Midgaard: your home city](#5-midgaard-your-home-city)
6. [Practice, train and gain: how your character grows](#6-practice-train-and-gain-how-your-character-grows)
7. [Combat basics](#7-combat-basics)
8. [How experience works](#8-how-experience-works)
9. [The levelling roadmap: where to go, levels 1 to 101](#9-the-levelling-roadmap-where-to-go-levels-1-to-101)
10. [Equipment and gearing](#10-equipment-and-gearing)
11. [Quests, autoquests and the two level quests](#11-quests-autoquests-and-the-two-level-quests)
12. [Death and recovery](#12-death-and-recovery)
13. [Money, banks and shopping](#13-money-banks-and-shopping)
14. [Getting around: boats, flying, mazes and maps](#14-getting-around-boats-flying-mazes-and-maps)
15. [Other players: channels, groups, clans and PK](#15-other-players-channels-groups-clans-and-pk)
16. [Hero and beyond: tiers, advance and reroll](#16-hero-and-beyond-tiers-advance-and-reroll)
17. [Quick reference card](#17-quick-reference-card)

---

## 1. MUDs for MMO players

A MUD is an MMO made entirely of text. Most of what you already know carries over; it's just presented differently.

| MMO concept | How it works here |
|---|---|
| The world map | The world (called **Thera**) is a grid of **rooms**. Each room has a description and **exits** (north, east, south, west, up, down). You move one room at a time by typing a direction. |
| Your screen | Everything arrives as text. The line ending in `>` is your **prompt**, which shows your hit points, mana and movement, e.g. `<100hp 100m 100mv>`. |
| Health, mana and stamina | **hp**, **m** (mana) and **mv** (movement). Walking costs movement points; when they hit 0 you can't move until they recover. |
| Regeneration | Stats come back on a timer called a **tick** (about once a minute). Use `rest` or `sleep` to regenerate much faster, and `stand` or `wake` to get up again. |
| Mouse-over / inspect | `look`, `look <thing>`, `examine <thing>`. |
| "Con" colours | `consider <monster>` (see [section 7](#7-combat-basics)). |
| Aggro | **Aggressive** monsters attack you as soon as you walk in. Everything else waits for you to attack. |
| Loot window | Monsters leave a **corpse**. With the auto-options that are on by default, you automatically loot gold and items and sacrifice the empty corpse. |
| Hotbar abilities | Typed commands: `kill rabbit`, `cast 'magic missile' rabbit`, `bash`, `flee`. Spell names longer than one word need quotes. |
| Hearthstone | `recall` (or `/`) teleports you back to your home temple. |
| Trainers and talent points | **Practices** improve skills; **trains** improve stats, hp and mana. See [section 6](#6-practice-train-and-gain-how-your-character-grows). |
| Spirit healer, corpse run | Your corpse is moved to a **morgue** in town automatically. See [section 12](#12-death-and-recovery). |

**Useful habits from minute one:**

- `help <anything>` is the in-game manual. `commands` lists every command, and `socials` lists the emotes.
- Commands can be abbreviated: `n` for `north`, `l` for `look`, `inv` for `inventory`, `eq` for `equipment`, `sc` for `score`. When an abbreviation is ambiguous, the game uses the first command that matches.
- `!` repeats your last command.
- `scroll 0` turns off the `[Hit Return to continue]` pager. Do this if your client scrolls fine, because the pager quietly swallows whatever you type next.
- `prompt` changes your prompt, for example `prompt <%hhp %mm %vmv %Xtnl>` adds experience to next level (`help prompt` lists the codes).
- `colour` toggles colour.
- A MUD client helps a lot. **Mudlet**, **TinTin++** and **MUSHclient** all offer speedwalking, aliases, triggers and maps. The game sends GMCP data (vitals, room info for mappers, channels), offers UTF-8 and compresses its output with MCCP; see `help gmcp`. Set your client to UTF-8 if the login screen looks garbled.

---

## 2. Reading this guide

- **Routes** use speedwalk notation and, unless stated otherwise, **start at the Temple of Thoth** (where `recall` takes good and neutral characters once they're level 10). `2s 5w` means type `s` twice, then `w` five times. Directions are `n e s w u d`.
- If a route stops at a door, type `open <direction>` (e.g. `open south`) and continue.
- **Lost?** `guide <area>` gives directions to any area from wherever you are (for example `guide moria`), taking recall, doors, boats and flying into account. `guide` on its own lists the areas for your level.
- **Monster levels** in the tables are the range most monsters in that area fall into (the middle half), so a "12–16" zone may still have a few stronger or weaker monsters. "Aggressive" counts how many of the area's monsters attack on sight.
- Level numbers here are what the game uses internally. In play you never see a monster's level; use `consider`.

---

## 3. Character creation, step by step

Connect, and the game walks you through these prompts in order.

### 3.1 Name

Pick a name that fits a fantasy setting. The welcome screen warns: *"'RoT2' REQUIRES role-playing type names... an IMM WILL delete you."* You can't use a name that matches a monster's name, and you'll be asked to confirm it.

### 3.2 Password and sex

Type a password twice. Sex (`M`/`F`) is cosmetic apart from titles.

### 3.3 Alignment: (L)ight, (S)hadow or (N)eutral

| Choice | Starting alignment | Home temple (where `recall` and death take you after level 10) |
|---|---|---|
| **L**ight | +750 (good) | Temple of Thoth |
| **N**eutral | 0 | Temple of Thoth |
| **S**hadow | −750 (evil) | Temple of Belan (a twin of Thoth's temple in the same spot; see [section 5](#5-midgaard-your-home-city)) |

Why it matters:

- **Equipment:** some items are anti-good, anti-evil or anti-neutral. If you try to wear one that clashes, it **zaps you and drops to the floor**.
- **Experience:** good characters get up to +33% experience for killing evil monsters, and evil characters the same for killing good ones. Neutral characters get +33% for killing strongly aligned monsters of either kind, but only **half** experience for killing other neutrals.
- **Drift:** killing a monster much more evil than you pushes you toward good, and killing one much more good pushes you toward evil. Killing monsters close to your own alignment slowly pulls you toward neutral. Light characters who mostly kill evil things stay good.
- **Changing it later** is cheap: the priests in Thoth's and Belan's chapels shift you 200 points for 20 gold ([5.4](#54-the-chapels-alignment-sanctuary-and-blessings)).

**Recommendation for a first character: Light.** The level-1 to 50 zones are full of evil monsters (orcs, trolls, undead, drow), so a good character earns bonus experience almost everywhere.

### 3.4 Race

Your race sets your starting stats, your stat caps, some free skills and natural abilities, and an **experience cost**: how many experience points each level takes. The table shows experience per level when you don't customise ([3.6](#36-customize-yn)). Lower is faster.

| Race | Pts | Mage | Cleric | Thief | Warrior | Ranger | Druid | Vampire | Savage | Squire |
|---|---|---|---|---|---|---|---|---|---|---|
| human | 0 | **1000** | **1000** | **1000** | **1000** | **1000** | **1000** | **1000** | **1000** | **1000** |
| halfelf | 2 | 1155 | 1155 | 1155 | 1155 | 1155 | 1155 | 1155 | 1100 | 1265 |
| gnome | 4 | 1200 | 1320 | 1800 | 1800 | 1500 | 1260 | 1800 | 1200 | 1500 |
| elf | 5 | 1250 | 1562 | 1250 | 1500 | 1500 | 1312 | 1437 | 1250 | 1250 |
| halfling | 5 | 1312 | 1500 | 1250 | 1875 | 1875 | 1500 | 1500 | 1250 | 1875 |
| goblin | 5 | 1312 | 1562 | 1375 | 1562 | 1500 | 1500 | 1375 | 1250 | 1937 |
| giant | 6 | 2600 | 1625 | 1950 | 1365 | 1625 | 1950 | 1560 | 1300 | 1560 |
| cloud giant | 6 | 2600 | 1625 | 1950 | 1365 | 1625 | 1950 | 1560 | 1300 | 1560 |
| pixie | 6 | 1300 | 1300 | 1560 | 2600 | 1950 | 1300 | 1950 | 1300 | 1820 |
| halforc | 6 | 2600 | 2600 | 1560 | 1300 | 1625 | 1950 | 1365 | 1300 | 1820 |
| satyr | 6 | 1430 | 1430 | 1430 | 2275 | 1430 | 1430 | 1950 | 1300 | 2210 |
| gnoll | 7 | 1485 | 1485 | 1687 | 1485 | 2362 | 1485 | 1485 | 1350 | 1822 |
| minotaur | 7 | 1485 | 1485 | 1485 | 1282 | 1485 | 1485 | 1485 | 1350 | 1552 |
| dwarf | 8 | 2100 | 1400 | 1750 | 1400 | 1540 | 1540 | 1540 | 1400 | 1540 |
| centaur | 9 | 1450 | 1595 | 1450 | 2537 | 1595 | 1595 | 1377 | 1450 | 1812 |
| draconian | 11 | 1937 | 2325 | 3100 | 1550 | 1705 | 1937 | 2325 | 1550 | 2092 |
| titan | 11 | 2790 | 1627 | 2015 | 1627 | 1627 | 2015 | 1550 | 1550 | 2635 |
| demon | 20 | 2000 | 2000 | 2000 | 2000 | 2000 | 2000 | 2000 | 2000 | 2900 |
| gold dragon | 25 | 2500 | 2500 | 2500 | 2500 | 2500 | 2500 | 2500 | 2500 | 3000 |

What each race brings (stats are Str/Int/Wis/Dex/Con; "max" is the most you can train to, and your class's prime stat can go 2 higher, or 3 for humans):

| Race | Start stats | Max stats | Free skills and natural abilities | Weaknesses |
|---|---|---|---|---|
| human | 13/13/13/13/13 | 18 all | Cheapest experience; +3 to the prime-stat cap | none |
| elf | 12/14/13/15/11 | 16/20/18/21/15 | sneak, hide; night vision; resists charm | iron |
| dwarf | 14/12/13/11/15 | 20/16/19/15/21 | berserk; night vision; resists poison and disease | drowning |
| giant | 16/11/13/11/14 | 22/15/18/15/20 | bash, fast healing; resists fire and cold | mental, lightning |
| pixie | 10/15/15/15/10 | 14/21/21/20/14 | **flies permanently**, detects magic, night vision; resists charm and mental | iron |
| halfling | 11/14/12/15/13 | 15/20/16/21/18 | sneak, hide; **pass door**; resists poison and disease | light |
| halforc | 14/11/11/14/15 | 19/15/15/20/21 | fast healing; berserk; resists magic and weapons | mental |
| goblin | 11/14/12/15/14 | 16/20/16/19/20 | sneak, hide; night vision; resists mental | silver, light, wood, holy |
| halfelf | 12/13/14/13/13 | 17/18/19/18/18 | farsight | none |
| gnome | 11/15/14/12/12 | 16/20/19/15/15 | night vision; resists mental | drowning |
| draconian | 16/13/12/11/15 | 22/18/16/15/21 | fast healing; **flies**; immune to poison and disease; resists fire and cold | slash, pierce, lightning |
| centaur | 15/12/10/8/16 | 20/17/15/13/21 | enhanced damage | none |
| gnoll | 15/11/10/16/15 | 20/16/15/20/19 | detects hidden, dark vision | silver |
| cloud giant | 16/11/13/11/14 | 22/15/18/15/20 | bash, fast healing; **flies**, farsight; resists bash | fire |
| demon | 20/20/20/20/20 | 25 all | sneak, backstab, second attack, hide, fast healing; **flies**, detects invisible and hidden; resists fire and magic | cold, light |
| gold dragon | 20/20/20/20/20 | 25 all | same five skills as demon; **flies**, detects invisible and hidden; resists lightning, cold and magic | fire, acid |
| minotaur | 18/11/10/11/17 | 23/16/15/16/22 | enhanced damage; farsight; immune to poison | bash |
| satyr | 18/14/5/9/16 | 23/19/10/14/21 | detects hidden, evil and good; immune to fire | holy, light |
| titan | 20/13/13/10/20 | 25/18/18/15/25 | fast healing; detects invisible; berserk; immune to charm | none |

Race tips:

- **Human** is the best choice for learning: every class levels at the minimum 1,000 experience per level, and humans get the highest cap on their class's prime stat.
- **Flying races** (pixie, draconian, cloud giant, demon, gold dragon) never need a boat or a flying potion, so every water and sky zone in [section 14](#14-getting-around-boats-flying-mazes-and-maps) is open to them from level 1.
- **Demon and gold dragon** are power picks: stats of 20 across the board, five free combat skills and built-in flight. You pay with 2 to 2.5 times the experience per level of a human, for every level all the way to 101.
- `help race` lists every race with its cost, and each race has its own entry (`help centaur`, `help cloud giant` and so on).

### 3.5 Class

There are nine first-tier classes, and `help <class>` describes each one. "HP per level" is the class's die roll before your constitution bonus, multiplied by roughly 1.6.

| Class | Prime stat | HP/level | Mana | Starting weapon | Plays like |
|---|---|---|---|---|---|
| **warrior** | Str | 13–18 | little | sword | The tank. Best hit points, second, third and fourth attack, bash, parry, rescue, all weapons. **Easiest first character.** |
| **squire** | Con | 10 | little | sword | Same default skill package as the warrior, with Con as prime stat. Its base skills are the brawler set (hand to hand, kick, trip, gouge) instead of the warrior's second attack and dual wield. |
| **savage** | Str | 10–12 | little | sword | Unarmed brawler: hand to hand, kick, trip, gouge, dodge, fast healing, plus utility magic (enhancement, detection, transportation). |
| **ranger** | Str | 9–13 | yes | spear | Fighter with healing, curative and transportation magic, track, and earthquake. |
| **thief** | Dex | 8–13 | little | dagger | Backstab, circle, sneak, hide, pick lock, steal, peek, dodge, second attack. |
| **vampire** | Con | 6–8 | yes | dagger | Thief-style fighter with strong accuracy plus mind and illusion magic and `feed`. Low hit points. |
| **cleric** | Wis | 7–10 | yes | mace | Healer and protector: heals, sanctuary, benedictions, curatives, decent melee. Very forgiving solo because it can heal itself. |
| **druid** | Wis | 7–10 | yes | polearm | Healing magic plus real attack spells (combat, meteor, harm); second attack. |
| **mage** | Int | 6–8 | yes | dagger | Strongest offensive magic, plus protective, shielding, illusion and transport groups. Enchanting is available through customisation. Levitates its shield, so both hands stay free for weapons. Fewest hit points; fragile early. |

Every class also gets *recall, scrolls, staves and wands* free, and can use `class <classname> skill` or `showclass <class>` in game to see exactly which skills it gets at which level.

**Recommended first characters:** human warrior (simplest), human cleric (self-healing, very hard to kill), or human ranger (melee plus healing).

### 3.6 Customize (Y/N)?

- **N** (recommended) gives you your class's **default package**, a balanced set of skills costing 40 creation points, and the experience per level shown in the table above.
- **Y** opens the skill shop. `list` shows groups and skills with their costs, `info <group>` shows what's inside, `add`/`drop` buy and remove, `premise` explains the system, and `done` finishes. Every point over 40 makes **every level** cost more (50 points is 1,500 per level and 60 points is 2,000, before your race multiplier), and expensive skills are slower to practise. Going **under** 40 doesn't help: experience per level never drops below the 40-point rate, and new characters get 30 training sessions either way.

The creation screen claims the skills you pick are "the only skills you will ever learn". That isn't quite true: you can buy more later with training sessions using `gain` ([section 6](#6-practice-train-and-gain-how-your-character-grows)), and buying them later doesn't raise your experience per level.

### 3.7 Weapon

Pick your starting weapon skill from the list offered. It starts at 40%. Match it to the weapon you'll actually use: warriors and squires should take sword (the starting and pack weapons are swords), mages and thieves dagger, clerics mace, and so on.

Then read the message of the day, press Return, and you're in.

---

## 4. Your first hour: gearing up and the Mud School

### 4.1 What you start with

Checked on a fresh human warrior:

- **100 hp, 100 mana, 100 movement.**
- **30 training sessions and 35 practice sessions**, already unspent. Use them now ([4.3](#43-spend-your-30-trains-and-35-practices-now)).
- +3 to your class's prime stat.
- Wearing: a holographic war banner (light), a sub-issue kevlar vest, a sub-issue riot shield and your class's sub-issue weapon. `outfit` will replace any of these if you lose them, up to level 9.
- Carrying: a **survival pack** full of gear, three maps (Midgaard, Western Thera and Eastern Thera), and a **green quest pouch**. Keep the pouch; you'll need it for the level quests ([section 11](#11-quests-autoquests-and-the-two-level-quests)).
- All the convenience settings are on: auto-assist, auto-exits, auto-gold, auto-loot, auto-sacrifice, auto-split and auto-store (`autolist` shows them).

You start at the **Mud School's entrance checkpoint**. Mud School is a cyberpunk training facility. Its room descriptions colour-code what matters: cyan for directions, yellow for things to `look` at, magenta for people and creatures, green for commands, red for warnings (`look legend` at the entrance).

### 4.2 Unpack the survival pack (don't skip this)

The pack holds a **complete set of armour and a better weapon**, all level 5. That's low enough for a level-1 character to wear, because first-tier characters can wear anything of level 19 or lower ([section 10](#10-equipment-and-gearing)). In testing it raised a new warrior's maximum hp from 100 to 150, strength from 16 to 20 and dexterity from 13 to 17.

There are three traps, all found in testing:

1. `get all pack` fails partway because you can't carry everything at once.
2. `wear all` won't replace something you're already wearing, and it will try to wear the pack itself as a cloak.
3. One item, the **Blackened Sphere**, is an *exotic weapon* with −2 dexterity and −50 movement. Leave it in the pack until you're much higher level.

Do it in this order instead:

```
scroll 0
look in pack
get all pack
wear all
remove pack
get boots pack
wear boots
get helmet pack
wear helmet
get gloves pack
wear gloves
get visor pack
wear visor
get shroud pack
wear shroud
get 'small metal shield' pack
wear shield
wear piecemeal
```

(The breastplate's keyword is `piecemeal`, not "plate".) Then, depending on class:

- **Sword users:** `remove sword` and `wield 'ancient sword'`. The Ancient Sword is a 3d5 sword and beats the sub-issue sword (`compare sword` will tell you so).
- **Dagger users:** `wield 'ancient dagger'`.

Put anything left over back with `put <item> pack`. The pack also holds seven pot pies and a barrel of water (food and drink), a lava lamp (a light) and a belt pouch (a container).

Check the result with `equipment` and `score`.

### 4.3 Spend your 30 trains and 35 practices now

The Mud School has its own trainer and practice master. From the Mud School entrance:

| Where | Route from the Mud School entrance | What it's for |
|---|---|---|
| Furey's conditioning lab (trainer) | `n w` | `train` |
| Zump's uplink room (practice master) | `n e` | `practice` |
| Med bay | `e` | A street doc who sells spells, and faster healing |
| Donation room | `w` | Free hand-me-down gear |
| Mud School Morgue | `2e` | Your corpse goes here if you die below level 10 |

**Training** ([section 6](#6-practice-train-and-gain-how-your-character-grows) has the full rules): your **prime stat costs 1 session per point, other stats 2**, and **+10 hp, +10 mana or +10 movement costs 1**. A solid plan for 30 sessions:

1. Raise your **prime stat** to its maximum (it's cheap, and it's your class's main stat).
2. Raise **Constitution** (hit points every level) and **Wisdom** (practices every level; 15 Wis gives 2 per level and 18 gives 3).
3. Put the rest into **hp**. Casters can split it with mana.

**Practising:** type `practice` to list your skills, then `practice <skill>` to spend one session on it. Each session adds a percentage based on your Intelligence, up to a cap of **75%**; after that, skills only improve by using them. Spend your 35 now on the skills you'll use every fight: your weapon, your main attack spell or skill, and defensive skills such as parry, dodge and shield block.

### 4.4 Walking the Mud School

The school is a short tutorial. Signs on the walls explain each step (`look sign`). The main path from the entrance is `n` (induction lobby) → `n` (gear check, with a plaque) → `w` (the **nav-grid hub**: practise moving in every direction, then go `n`) → `n` (a sign about `score`) → onward to the combat lessons.

- **Lesson: running away.** Go `down` from the combat briefing room, `consider` the **nanite blob**, `kill blob`, then `flee`. The blob is too strong to beat; it exists so you can practise fleeing. Don't stay to the finish.
- **The containment pods.** Below the next station (the Containment Bay) are four tethered **training constructs** (keyword `monster` or `construct`). Their internal levels are 40–65, but they have **small hit points** (roughly 6 to 65). Because experience depends on level, not hit points, each one is worth an enormous amount of experience at level 1. Kill them all (they carry gear you need), but note that two of them are aggressive.
- **The supply kiosk** sells a water skin and a lantern.
- **The blackout room** needs a light (your war banner works). Its **loader mech** carries gloves, sleeves, a bracer and a keycard; the hatch beyond is jammed open, so you don't need the keycard.
- **The Graduation Dais** has the field medic of Thoth and the **diploma daemon**, which holds your certification chip (+1 Con and +1 Wis while held).

South of the entrance (`open south`, then `s`) is the **Sim Arena**. It has a holo-rabbit, lizard drone, armoured boar, chrome fox and cyber-snail, all with high internal levels and very little hp, so they're excellent early experience. Below the arena is the **maintenance sublevel**: a security bear (about 80 hp), a cyber-wolf, and **the scavenger beast**, which is aggressive and has around 150 hp. Leave the beast until you've gained a few levels.

Your corpse goes to the Mud School Morgue if you die before level 10, and `recall` brings you back to the Mud School entrance until level 10. You can't enter the school after level 9, so get everything you want from it first.

**To reach Midgaard from the Mud School entrance:** `d e 7n` takes you down the stairs, through the park and up the main street to the Temple of Thoth.

---

## 5. Midgaard: your home city

Midgaard is the hub. All routes here start at the **Temple of Thoth** (room 3001).

### 5.1 Essential stops

| Place | Route | Why you'd go |
|---|---|---|
| **Temple Altar** (healer) | `n` | Paid healing ([7.5](#75-healing-and-resting)) |
| Rainbow Bridge to **Heimdall** | `n 3u` | Autoquests and the level-50 and level-100 **level quests** ([section 11](#11-quests-autoquests-and-the-two-level-quests)) |
| **City Morgue** | `e` | Your corpse appears here after you die (level 10 and up) |
| **Donation Room** | `w` | Free gear other players gave away. Give yours with `donate <item>`. |
| Temple Square (fountain) | `s` | Free drinking water: `drink fountain` |
| **Market Square: the Dungeonmaster** | `2s` | **One-stop shop:** `train`, `practice`, `gain`, and `quest` ([section 11](#11-quests-autoquests-and-the-two-level-quests)) |
| **The Forger** | `s e n` | Add elemental effects to a weapon for 1 platinum each ([10.5](#105-forging-the-cheapest-big-upgrade)) |
| Temple of Belan (evil characters' home temple) | not reachable on foot from Thoth; evil characters arrive by `recall` or death | Its exits lead into the same morgue (`e`), Temple Square (`s`) and donation room (`w`) as Thoth's. It has its own altar healer (`n`) and a **guild master who trains, practises and gains** directly above it (`u`). |

### 5.2 Shops

| Shop | Route | Sells |
|---|---|---|
| General Store | `2s e n` | torches, lanterns, water skins, bags, boxes, gem pouches |
| Bakery | `2s w n` | food (pies, bread, cookies) |
| Weapon Shop | `2s 2e n` | dagger, swords, club, mace, axes, spear, staff, flail |
| Armoury | `2s w s` | scale (level 9) and chain (level 19) armour, shields |
| Leather Shop | `3s 2w n` | full leather armour sets (level 0) |
| Magic Shop | `2s 2w n` | identify, cancellation and recall scrolls; see-invisible potions; a ring of protection; a wand of magic missiles |
| **Apothecary** (potion-brewer) | `3s 3e n` | healing and cure potions, **sanctuary**, armour, **flying**, true sight, antidotes |
| Jeweller | `2s e s` | gems, which are a light way to carry money, and the cubic zirconium clans use as currency |
| **The captain** (Levee) | `3s 2e s` | **raft and canoe**, the boats you need for deep water |
| Melancholy's Maps | `3s w n` | maps of Olympus, New Thalos, Moria, the Dwarven Kingdom and Midgaard |
| Pet Shop | `3s 2e n` | one pet at a time |
| First National Bank | `2s 3w 2n 2e s` | `deposit` and `withdraw` platinum ([section 13](#13-money-banks-and-shopping)) |

The bars around town (the Grunting Boar, the guild bars, Grubby Inn) sell drinks.

### 5.3 Guilds and trainers

Any practice master will teach any class. You don't have to visit your own guild, and the **Dungeonmaster in Market Square (`2s`) handles practising, training and gaining all in one place**. For reference:

| Guildmaster | Route |
|---|---|
| Cleric (Cleric's Inner Sanctum) | `s w n w` |
| Mage (Mage's Laboratory) | `2s 2w 2s e` |
| Warrior (Tournament and Practice Yard; trains too) | `2s 2e s e s` |
| Thief (The Secret Yard) | `3s e s e s` |
| Ranger (Ranger's Study) | `3s e 2n e` |
| Druid (Druid's Holy Sanctum) | `2s 3e 2s 2e s` |
| Vampire (Vampire's Crypt) | `s e d n e` |
| Sailor (trainer, Abandoned Warehouse) | `3s 3e s` |

### 5.4 The chapels: alignment, sanctuary and blessings

Thoth's chapel (`2s 3e 3n w s`) and Belan's chapel (`2s 3e 3n w n`) each have a High Priest. Type `repent` (Thoth) or `curse` (Belan) on its own to see the price list.

| At Thoth's High Priest | Cost | Effect |
|---|---|---|
| `repent align` | 20 gold | +200 alignment (toward good) |
| `repent bless` | 20 gold | casts *bless* on you |
| `repent sanctuary` | 35 gold | casts **sanctuary** on you (halves damage taken). Not for evil characters. |
| `repent voodoo` | 1 platinum | removes voodoo-doll curses |

Belan's High Priest offers the mirror image with `curse align` (20 gold, toward evil), `curse sanctuary` (35 gold, evil characters only) and `curse voodoo`.

**Sanctuary for 35 gold is one of the best deals in the game at low level.** Pick it up before heading out.

### 5.5 New Thalos, the second city

**New Thalos** lies straight east of Market Square (`2s 15e` reaches its west gate). It has its own guildmasters for the mage, cleric, warrior, thief, ranger, druid and vampire guilds (all of whom train, practise and gain), a bank, healers and shops. It's a good base for levels 15–30 and is also a levelling zone itself.

---

## 6. Practice, train and gain: how your character grows

Every level you get:

- **Hit points:** your class die roll plus a Constitution bonus, multiplied by about 1.6.
- **Mana:** based on Intelligence and Wisdom; non-casters get a third as much.
- **Movement:** based on Constitution and Dexterity.
- **Practices:** 0–5 depending on Wisdom (Wis 5–14: 1, 15–17: 2, 18–21: 3, 22–24: 4, 25: 5).
- **1 training session.**

A level-up also heals you a good deal and cures poison, plague, blindness, sleep and curse.

### `practice`: improving skills and spells

At any practice master (the Dungeonmaster, any guildmaster, or Zump's uplink room in the Mud School), `practice <skill>` spends one practice session. How much each session adds depends on your **Intelligence** and the skill's difficulty for your class. You can practise up to **75%**; beyond that, skills improve only by using them in play, up to 100%. You can only practise skills you have reached the level for (`skills`, `spells`, `class <name> skill`). `practice` with no argument lists your skills and spells with your current percentages.

### `train`: improving stats, hp, mana and moves

At a trainer (the Dungeonmaster, the warrior guildmaster, the sailor, or Furey in the Mud School's conditioning lab):

| You train | Costs | Gives |
|---|---|---|
| Your class's **prime** stat | 1 session | +1 |
| Any other stat | 2 sessions | +1 |
| `hp` / `mana` / `move` | 1 session | +10 |

Stats cap at your race's maximum, plus 2 on your prime stat (3 for humans). `train` with no argument lists what you can still raise.

### `gain`: buying new skills later

At a `gain` trainer (the Dungeonmaster, the New Thalos guildmasters, or Twinkletoes in the Faerie Ring):

| Command | Effect |
|---|---|
| `gain list` | Skills and groups you can buy, with costs in training sessions. A ✓ means you can use it as soon as you gain it; a grey number is the level you must reach first (for a group, when the first part of it becomes usable). |
| `gain <name>` | Buy it. This doesn't raise your experience per level. |
| `gain convert` | 5 practices → 1 training session (you need at least 6 to start) |
| `gain study` | 1 training session → 5 practices |
| `gain quest` | 3 autoquest points → 1 training session |
| `gain points` | Lower your creation points by 1 (costs 1 session), making every future level cheaper. Not below 40, not on a level quest, and only when you're within 5,000 experience of your next level |

---

## 7. Combat basics

### 7.1 Starting, watching and ending a fight

- `consider <target>`: always do this first. Here it compares **hit points, armour, damage, accuracy and strength, not level**, so it tells you how hard the fight is, not how much experience it's worth. From easiest to hardest: *"You can kill $N naked and weaponless"*, *"no match for you"*, *"looks like an easy kill"*, *"The perfect match!"*, *"Do you feel lucky, punk?"*, *"laughs at you mercilessly"*, *"Death will thank you for your gift."*
- `kill <target>` starts a fight (`murder` is for players). Combat rounds then run automatically about every 4 seconds; you type skills and spells in between.
- `flee` attempts to escape and **costs 10 experience**. It's your main emergency button.
- `wimpy <hp>` makes you flee automatically below that hp. `wimpy` on its own sets it to 20% of your maximum. **Set it.**
- `recall` during a fight works only some of the time: your chance is 80% of your recall skill, and new characters start at 50% skill (so about 40%). It improves as you use it. A successful recall costs 25 experience. Fleeing first is still the safer bet.
- `rescue <ally>` takes the monster's attention off a group member.

### 7.2 Fighting stances

RoT has martial-arts stances that are easy to overlook. `stance <name>` sets one; `autostance <name>` enters it automatically whenever a fight starts. Stances level up from 0 to 200 by fighting in them (`sskill` shows your progress).

- **Basic:** serpent (fast and aggressive), crane (blocking), crab (low, damage-reducing), mongoose (dodging), bull (raw power).
- **Advanced** (each needs two basic stances at grand master): mantis (crane + serpent), dragon (bull + crab), tiger (bull + serpent), monkey (crane + mongoose; cancels the opponent's stance bonus), swallow (mongoose + crab; the most defensive).

`help styletable` shows which stance beats which. Fighting with no stance is a real disadvantage, so `autostance bull` or `autostance serpent` from level 1 costs nothing and starts training them.

### 7.3 Damage words

Hits are described in words that map to damage ranges. For example, *scratch* is up to 4, *wound* up to 20, *DEVASTATE* up to 75, *OBLITERATE* up to 100, and anything over 150 is *UNSPEAKABLE*. See `help damage` for the full list.

### 7.4 Useful commands mid-fight

`mock <target>` shows how much damage you would do, without actually hitting. `scan` looks into adjacent rooms. `where` shows who's in the area. `affects` lists the spells currently on you.

### 7.5 Healing and resting

- `rest` or `sleep` between fights; you regenerate much faster. Ticks happen about every minute.
- **Healers** sell spells: type `heal` near one to see the list. The temple altar healer (`n` from the temple) charges cure light 10 gold, cure serious 15, cure critical 25, heal 50, refresh 5, restore mana 10, and cure blindness, disease, poison and curse 15–50 gold.
- Eat and drink. Hunger and thirst are real; the pack's pot pies and water barrel last a while, and the Temple Square fountain is free.

---

## 8. How experience works

Experience per kill depends on the **level difference** between you and the monster:

| Monster vs you | Base experience |
|---|---|
| 10 or more levels **below** | **0**. Leave the area. |
| 5 below | 22 |
| equal | 95 |
| 4 above | 181 |
| every level above that | +29 more each |

On top of that:

- **Below level 11** you get a big bonus (×15/(level+4), so 3× at level 1). This is why the Mud School's high-level, low-hp critters level you so quickly.
- **Alignment**: up to +33% for killing opposite-aligned monsters; neutrals get half for killing other neutrals ([3.3](#33-alignment-light-shadow-or-neutral)).
- **Above level 60** experience per kill shrinks (×15/(level−25), so about a third at level 70 and a fifth at level 100). Expect the last 40 levels to be slow, and lean on higher-level zones and quests.
- **Groups** split experience by level.
- Every reward varies randomly by ±25%. There's no penalty for killing the same kind of monster over and over.

You lose experience by fleeing (10), recalling out of a fight (25), dying ([section 12](#12-death-and-recovery)), and from some spells. `score` shows how much you need for the next level. Your experience per level is fixed at creation by race, class and creation points ([3.4](#34-race)).

**Rule of thumb:** fight monsters that `consider` rates as *"easy kill"* to *"perfect match"* in zones whose level range is at or slightly above your own.

---

## 9. The levelling roadmap: where to go, levels 1 to 101

How to read the tables:

- **Levels** = the range most of the area's monsters fall into.
- **Aggr** = aggressive monsters / total monsters.
- **Route** is from the Temple of Thoth, and every route was walked in a test copy of the game to confirm it.
- **Boat** routes cross deep water: carry a raft or canoe from the captain (`3s 2e s`) or be flying. **Fly** routes need flying the whole way: a potion of flying from the apothecary (`3s 3e n`), the *fly* spell, or a flying race.
- 🌀 marks routes that pass through the **Shadow Grove**, a maze whose exits reshuffle every time the area resets ([14.3](#143-mazes)). The route gets you to the grove; from there you have to find your own way through.
- **Soft targets**, under each table, are monsters with unusually few hit points for their level. Experience depends only on a monster's level and alignment, never its hit points ([section 8](#8-how-experience-works)), so these pay the most experience for the least fighting.
  - Most monsters' hit points follow a standard table for their level (about 80 at level 10, 390 at 30, 1,000 at 50, 2,100 at 70 and 6,300 at 100), so some bands have no real outliers. Where that's the case, the band says so.
  - Hit points are averages, and ×4 means four of them spawn. Shopkeepers, trainers, healers and monsters in safe rooms are left out.
  - *aggressive* attacks on sight; *flees* runs when hurt, which costs you time; *steals*, *poison* and *casts* are special attacks. *Sanctuary* halves your damage, and *ice, fire* and *shock shields* hurt you every time you land a hit (5–15, 10–20 and 15–25 hp each).

Below level 10, `recall` returns you to the Mud School, so plan to walk back to town.

### Levels 1–9: Mud School, then the starter zones

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Mud School** | tutorial | 3/18 | you start here | Do the cages and the Arena first ([4.4](#44-walking-the-mud-school)) |
| **Smurfville** | 1–6 | 0/21 | `2s 7e n` | Nothing aggressive. The safest first zone. |
| **Day Care** | 3–6 | 2/25 | `2s 6e 3n 2e s` | Has a small shifting maze |
| **Mob Factory** | 5–12 | 5/33 | `3s 3w s e` | Close to town |
| **Haon Dor** (forest) | 4–9 | 15/23 | `2s 5w` | Just outside the west gate; many aggressive monsters |
| **Graveyard** | 5–7 | 13/14 | `6s 2e 2s w s` | Nearly everything is aggressive undead |
| **Shire** | 6–15 | 1/85 | `2s 5w n` | Huge and peaceful. Excellent for levels 5–12. |
| **Gnome Village** | 6–13 | 16/65 | `2s 8e s` | The damp hallways are a shifting maze |

**Soft targets** (a typical level-5 monster has about 28 hp):
- **Mud School** first: the containment pods and the Sim Arena are the softest monsters in the game ([4.4](#44-walking-the-mud-school)).
- **Mob Factory**: factory workers (level 5, 11–15 hp, ×11, flee).
- **Haon Dor**: cute rabbits (1, ~6 hp, ×4), large grey wolves (5, ~15 hp, ×4, aggressive) and ferocious wargs (9, ~35 hp, ×2, aggressive).
- **Smurfville**: the named smurfs (5–6, 11–21 hp) and plain smurfs (1–2, 6–11 hp, ×11). They all flee and pick pockets, so keep your gold in the bank.
- **Gnome Village**: hobgoblin soldiers (6, ~21 hp, ×12, aggressive).

### Levels 10–15

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Gangland** | 9–16 | 23/91 | `6s e 3s e` | Street gangs south of town |
| **Elemental Canyon** | 7–20 | 1/121 | `2s 6e 4s 2e s 2e d s` | 121 monsters, almost none aggressive. A great grinding spot. |
| **Crystalmir Lake** | 7–26 | 9/37 | `2s 6e 10n 2e 6n w` | Also the gateway to Solace and Yggdrasil |
| **Dragon Cult** | 8–15 | 9/22 | `4s w n` | |
| **Faerie Ring** | 10–15 | 0/18 | `6s 2e 3s 2w 2s 2e 2s e` | Peaceful. Twinkletoes in the bar below is a `gain` trainer. |
| **Miden'nir** | 12–16 | 9/16 | `6s 2e 3s 2w 2s` | Out the south gate to the Trail to Miden'nir; the forest starts one room east |
| **New Ofcol** | 9–38 | 5/67 | `2s 4e 3n 2w 3n e 2n 2e n e 3n 2e` | A town with a wide range of monsters |
| **Troll Den** | 5–14 | 18/18 | `2s 11w 2s w s w s 2w s e s` | Everything is aggressive; bring a group |
| **Chapel** | 8–19 | 36/46 | `6s 2e 2s w 6s` | Mostly aggressive |
| **Sewers** | 7–23 | 42/57 | `s w n w d` | Through the Cleric's Inner Sanctum and down the well. **The well is one-way**: recall out. |
| **Valley of the Elves** | 11–16 | 33/48 | `2s 4e 3n 2w 5n w n` | |
| **Moria** | 11–18 | 41/65 | `2s 6e 6n` | Out the east gate and north through the hills to Moria's cave. Lots of aggressive orcs. Better at the top of this band. |
| **Dark Continent** | 7–15 | 2/11 | Boat: `2s 15e 3n 4e 3s 7e n 2e` | |

**Soft targets** (a typical level-12 monster has about 100 hp):
- **Valley of the Elves**: valley elves (11, ~58 hp, ×5, flee) and valley elf scouts (11, ~68 hp, ×5, aggressive). A few of the valley's other aggressive monsters are far higher level, so stay near the elves.
- **Crystalmir Lake**: barracudas (10, ~47 hp, ×6, aggressive) in the lake's underwater rooms.

### Levels 15–20

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Mirkwood** | 10–20 | 9/14 | `2s 4e 3n 2w 2n 4e` | |
| **Holy Grove** | 10–25 | 2/14 | `2s 8e n` | |
| **Arachnos** | 12–25 | 5/27 | `2s 13w s 2w n w u w n` | Spiders |
| **Thalos** | 17–22 | 22/30 | `2s 6e s` | |
| **Wyvern's Tower** | 14–24 | 22/49 | `2s 6e 4s 2e s 2e d e` | |
| **New Thalos** (city) | 10–29 | 24/169 | `2s 15e` | Second city: guilds, bank, healers ([5.5](#55-new-thalos-the-second-city)) |
| **Sands of Sorrow** | 10–20 | 11/22 | Boat: `3s 2e 2s 3e` | |
| **Dragon Tower** | 13–36 | 28/53 | 🌀 via the Shadow Grove (route to its entrance under High Tower) | Somewhere beyond the maze |

**Soft targets:** none worth the trip. Hit points in this band follow the standard table almost exactly, so choose zones by the other columns.

### Levels 20–30

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Catacombs** | 18–24 | 49/70 | `2s 6e 3n 2e 3n 3w 2d` | Heavily aggressive undead |
| **Camelot** | 23–29 | 3/51 | `2s 7w n` | Peaceful and close. A favourite. |
| **Ancalador** | 20–27 | 32/48 | `2s 11w 2s w s e 2s w s` | |
| **Kerofk** | 18–36 | 21/105 | `2s 4e 3n 2w 5n e n` | Big area |
| **Marsh** | 18–32 | 28/37 | `2s 11w 2s w s w s 2w s w s` | |
| **Dwarven Kingdom** | 17–39 | 3/42 | `2s 6e 3n e` | Mostly peaceful dwarves |
| **High Tower** | 17–35 | 52/107 | 🌀 `2s 13w s 2w 2s w s 3w n w n` | The route reaches the Shadow Grove entrance; the tower is beyond the maze |
| **Pirate Lords** | 20–37 | 45/109 | `2s 6e 4s 2e s 2e d 3n e 3s e 2s w s e 2s 2e 2n 4e 2s 3e n` | Seas and isles. A long walk: expect to stop and rest on the way. |
| **Underground Tunnel** | 25–38 | 6/12 | `2s 6w d` | If the trapdoor down is closed, `open down` first |
| **Pyramid** | 15–35 | 10/45 | Boat: `3s 2e 2s 10e n e n 2e` | |
| **Astral Plane** | 22–33 | 29/62 | Fly: `s 2u n 2u` | Straight up into the sky from Temple Square |
| **Aarakocran City** | 26–35 | 16/45 | Fly: `2s 6e 4s 2e s 2e d s 4u n d 4n e 3n e u` | Bird-folk city with confusing corridors |
| **Galaxy** | 19–43 | 11/61 | 🌀 via the Shadow Grove (route to its entrance under High Tower) | A tavern beyond the maze |

**Soft targets:** few. The best is **Camelot**'s royal guards (27, ~255 hp, ×10, not aggressive), about a quarter below the usual 330 for their level.

### Levels 30–40

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Mirror Realm** | 25–45 | 11/65 | `2s 6e 2n e` | |
| **Jade Temple** | 25–45 | 52/75 | `2s 6e 6n e` | Mostly aggressive |
| **Drow City** | 27–45 | 24/25 | `2s 6e 4s 2e s 2e d w s 2d` | Nearly everything is aggressive |
| **Reverse Palace** | 30–40 | 1/75 | `2s 13w 3n` | Peaceful |
| **StoneBow Dale** | 21–52 | 0/49 | `6s 2e 3s 2w 8s` | No aggressive monsters. Has a bank and healers. |
| **City of Anon** | 8–50 | 1/109 | `2s 6e 4s 2e s 2e d 3n e 3s e 2s w s e 2s e` | Big city with a wide range of monsters |
| **Mega City One** | 19–39 | 5/27 | Boat: `3s 2e 2s 13e s` | |
| **Elvandar** | 35–40 | 1/28 | Boat: `3s 2e 2s 7w s` | |

**Soft targets:** few. The **Pirate Ship**'s sleepy pirates (38, ~530 hp, ×7, aggressive) have about a fifth less than the usual 680. The **Ancient Temple**'s aggressive training construct (40, 11 hp) is worth a detour, but there's only one.

### Levels 40–50

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Town of Solace** | 35–40 | 5/146 | `2s 6e 10n 2e 6n w d w n` | 146 monsters, mostly peaceful |
| **Yggdrasil** | 35–45 | 6/26 | `2s 6e 10n 2e 6n w d 3s` | The world tree |
| **Pirate Ship** | 35–47 | 23/66 | `2s 15e 3n 4e 3s 6e n` | |
| **Mahn-Tor** | 29–50 | 42/70 | `2s 6e 4s 2e s 2e d 3n e s` | |
| **Nirvana** | 27–56 | 38/43 | `2s 8e 2n 2e u` | Mostly aggressive |
| **Dylan's Area** (Witches Tower) | 40–46 | 43/47 | 🌀 through the Shadow Grove and High Tower | Almost all aggressive |

**Soft targets** (a typical level-45 monster has about 850 hp):
- **Ancient Temple**: the aggressive training construct (40, 11 hp) and an ancient lizard (50, ~30 hp). The lizard has sanctuary and ice, fire and shock shields, so each hit you land costs you 30–60 hp.
- **Divided Souls**: the black and grey assassins (50, ~110 and ~180 hp). They look like the best targets in the band, but they hit two to three times as hard as a normal level-50 monster.

**At level 50 you hit the first level quest.** Experience stops until you finish it ([11.3](#113-level-quests-at-50-and-100)).

### Levels 50–60

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Valley of the Titans** | 48–60 | 2/101 | `2s 13w 2n e n` | Large and peaceful. Has guildmasters. |
| **Cloudy Mountain** | 45–62 | 68/280 | `6s 2e 3s 2w 2s 2e s e` | Huge; many aggressive monsters |
| **Aerial City** | 50–65 | 10/45 | Fly: `2s 4e 3n 2w 3n e 2n 4e 4s 3e s` | Has a bank |

**Soft targets:** the Ancient Temple's ancient lizard and the Divided Souls assassins from the 40–50 band are still worth killing here, and from the late 50s the Ancient Temple's mummies (next band) start to pay.

### Levels 60–75

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Archonian Chessboard** | 50–90 | 0/45 | `2s 4e 3n 2w 3n e 2n 4e s e` | No aggressive pieces; very high hp |
| **Divided Souls** | 52–68 | 22/101 | 🌀 through the grove and the Galaxy tavern | |
| **The Abyss** | 50–80 | 38/46 | `2s 6e 4s 2e s 2e d s u n` | Mostly aggressive |
| **Ancient Temple** | 65–70 | 1/8 | `2s 13w u` | Small. Halen the healer is next door. |
| **UnderDark** | 68–78 | 16/396 | `4s d w d n 3d` | Enormous (almost 400 monsters) |
| **Olympus** | 15–101 | 9/41 | `2s 4e 3n 2w 6n` | Gods: most are high level |

**Soft targets** (a typical level-70 monster has about 2,100 hp):
- **Ancient Temple**, the best levelling spot in the game. Its "leveling mobs" have almost no hit points for their level: ancient mummies (70, ~40 hp, ×2, ice and shock shields), an ancient snake (68, ~45 hp) and three training constructs (65, ~28–65 hp; the wimpy ones flee). Nothing there is aggressive except a level-40 construct with 11 hp. In a test, a level-62 warrior with nothing better than a starter sword killed a mummy in two rounds, lost about 120 hp and earned 126 experience. Kill everything, then wait for the area to reset; Halen the healer is next door.

### Levels 75–90

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **The Mutant Dump** | 70–84 | 54/94 | `2s 15e 3n 4e s e` | Mostly aggressive |
| **Drakyri Isle** | 71–95 | 21/115 | `2s 13w s 2w n w n` | |
| **Elven Forest** | 70–101 | 60/136 | `2s 6e 4s 2e s w` | |

**Soft targets** (a typical level-90 monster has about 4,400 hp):
- **Fanatics' Tower**: the level-95 magic mages, listed as "L.95 Magic" (90, ~2,090 hp, ×5). They aren't aggressive, but they almost never miss, hit for about 120 and cast mage spells, so arrive at full health. The Adept of Eriana near the top heals.

### Levels 90–101

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **Hell** | 79–101 | 14/96 | `6s 2e 2s w 6s d s 2w 2s e n d n 2e s 4e 2s w 2s 2e d n e s e 2s n` | A long route through the Chapel that avoids Crystalmir Lake's maze rooms |
| **Fanatics' Tower** | 83–105 | 0/125 | `2s 15e 3n 2e 2n 2w u` | A tall tower with no aggressive monsters. The Adept of Eriana near the top trains, practises, heals and banks. |
| **Monster Guild** | 90–107 | 9/66 | `2s 5w 2n w` | |

**Soft targets:** the Fanatics' Tower mages from the 75–90 band are the only real outliers, and they stay worth killing up to level 100.

**At level 100 you hit the second level quest**; finishing it makes you a **Hero (level 101)**.

### Hero and beyond

| Zone | Levels | Aggr | Route | Notes |
|---|---|---|---|---|
| **The 36 Chambers of Death** | 160–200 | 38/38 | Boat: `3s 2e 2s 6w n w 3s 2e s e s 2w n` | Every monster is aggressive and far above Hero level. Group content. |

**Closed or unfinished areas** you may see in `areas`: Dreams, Palace of Tulqurin, The Hive, Death Knights, Lierknay Forest, Quifael's and "New area" have no entrance from the world. The Haunted House is the duel arena ([section 15](#15-other-players-channels-groups-clans-and-pk)).

---

## 10. Equipment and gearing

### 10.1 Slots

You have 21 equipment slots: light, two fingers, two necks, torso, head, legs, feet, hands, arms, shield, about body, waist, two wrists, primary weapon, held item, floating, **secondary weapon** (`second <weapon>`; anyone can, and the dual wield skill makes it swing more often) and **face**.

### 10.2 Who can wear what

- **Level:** a first-tier character can wear **any item of level 19 or lower, whatever their own level**. Above 19, the item's level must be at or below yours. (Second-tier characters: anything of level 27 or lower.) This is why the level-5 survival pack works at level 1, and why level-19 chain mail from the Armoury is fair game for a brand-new character with the money.
- **Shields:** a shield can't share your hands with a second weapon, or with a two-handed weapon, unless your class can **levitate** it in front of you. Mages and wizards can from level 1, priests from 25, liches from 40, clerics and striders from 50, vampires from 60 and rangers from 65. Third-tier characters also get it from a secondary mage at any level, cleric from 36, vampire from 46 or ranger from 76. Large races (giant, cloud giant, centaur, gnoll, minotaur, satyr, demon, draconian, gold dragon, titan) can always pair a two-handed weapon with a shield. See `help dual wield`.
- **Alignment:** items flagged anti-good, anti-evil or anti-neutral **zap you and fall to the floor** if they clash with your alignment.
- **Weight and count:** you can carry a limited number of items and a weight based on Strength (`score` shows both).
- **Newbie gear:** the "sub-issue" items from `outfit` can't be donated.

### 10.3 Judging items

- `compare <item>` compares an item with what you're wearing in the same slot, using weapon damage or armour class. It ignores bonuses such as +hp or +damage.
- `lore <item>` (a skill for mages, druids and others) and the **identify** scroll (Magic Shop) reveal an item's full stats.
- The flags in front of item names show their properties at a glance: `[V E B M G H Q]` = invisible, evil, blessed, magical, glowing, humming, quest item. `help flags` explains them, and `long` switches to the classic `(Glowing)` style.

### 10.4 Where gear comes from

1. **The survival pack** (levels 1–20).
2. **Midgaard shops:** the Armoury's chain set (level 19), the Leather Shop and the Weapon Shop ([5.2](#52-shops)).
3. **Monster drops:** auto-loot is on, so look at what you picked up with `inventory`.
4. **The donation pit** (`w` from the temple).
5. **Quest rewards** ([section 11](#11-quests-autoquests-and-the-two-level-quests)).
6. **The auction channel:** `auction` ([section 15](#15-other-players-channels-groups-clans-and-pk)).

### 10.5 Forging: the cheapest big upgrade

The **Forger** (`s e n` from the temple) enchants weapons for **1 platinum each**. The weapon must be in your **inventory, not wielded**:

```
remove sword
forge sword flame+
wield sword
```

`flame+` puts flame, drain, shocking, sharp and vorpal on in one go for **5 platinum**, the same as buying them one at a time. `frost+` does the same with frost instead of flame. Both skip anything the weapon already has.

The single options are `flame`, `frost`, `shocking`, `drain` (vampiric), `sharp` and `vorpal`. **They stack**, except that flame and frost won't share a weapon, and drain won't go on a blessed one. The enchantments wear off in time, so expect to come back. `help forge` lists everything. Do this as soon as you have a few platinum (your first quest pays enough; [section 11](#11-quests-autoquests-and-the-two-level-quests)), and again whenever you upgrade your weapon.

### 10.6 Other gear services

- `restring <item> <new name>` at any `gain` trainer (such as the Dungeonmaster, `2s`) renames an item's display name. It costs 5 autoquest points, and the item's keywords don't change.
- `sacrifice <item>` offers junk to your god for a small reward. Auto-sacrifice does this to empty corpses.
- `donate <item>` sends it to the donation pit; clan members can `cdonate` to their clan's pit.

---

## 11. Quests, autoquests and the two level quests

There are two quest-givers, and they do different things.

### 11.1 The Dungeonmaster: `quest` (Market Square, `2s`)

| Command | What it does |
|---|---|
| `quest request` | Get a quest: kill a named monster or recover an item. You have about 60–110 real minutes. |
| `quest info` / `quest time` | Remind you what the target is, and how much time is left. `score` shows the target, where to look and the time left too. |
| `quest complete` | Hand it in at the Dungeonmaster |
| `quest list` / `quest buy <item>` | Spend quest points |

The Dungeonmaster tells you the target's name, the room it was last seen in, and its area, e.g. *"Seek strange fish out somewhere in the vicinity of North shore of Crystalmir Lake... in the general area of Crystalmir Lake."* Look the area up in [section 9](#9-the-levelling-roadmap-where-to-go-levels-1-to-101) for directions. Targets aren't always matched to your level, so `consider` the target before attacking, and `quest quit` (with a small penalty) if it's beyond you.

**Rewards:** a kill quest pays 12–25 quest points and 5–24 platinum. A recovery quest pays 25–75 quest points and 5–34 platinum. Either has a 15% chance of 5–34 bonus **practices**. After completing a quest you wait about 25 minutes before the next; `score` shows the countdown. Your quest is lost if you log out, but you can request a new one straight away.

**The quest shop** (`quest list`): Sword (425), Amulet (375) or Shield (375) of the Ancients; a Decanter of endless drink (550); **70 practices for 500 points**; weapon and armour upgrades bought with global quest points (`wv1` +1 hit, `wv2` +1 damage, `av0`–`av3` +10 armour); and conversions between the different point types. From level 40, `quest buy experience` turns 1,000 platinum into 1,000 experience.

### 11.2 Heimdall: `aquest` (Rainbow Bridge, `n 3u`)

From **level 5**, Heimdall offers **autoquests**: retrieve a specific item from a monster that's between 2 levels below and 8 levels above you. He names the monster and the area. The **Dungeonmaster** (`2s`) is also a questmaster, so you can take and hand in autoquests at either of them.

To hand one in, stand in front of Heimdall or the Dungeonmaster and type `aquest` again (`quest complete` is only for the Dungeonmaster's own quests). The item must be the one you looted from the named monster, carried or worn, **not inside a bag**. You keep the item and get a **shimmering white pill**; eat it to bank autoquest points (used for restrings and conversions). If he says the quest isn't complete, check that the item isn't in a container.

### 11.3 Level quests at 50 and 100

When you earn enough experience to reach **level 51** or **level 101**, you **don't** level up. Instead you see:

> You must now complete a level quest to reach level 51

and your experience stops counting. To finish:

1. Go to **Heimdall** (`n 3u`) or the **Dungeonmaster** (`2s`) and type `aquest`. He names a unique item, the monster carrying it, and its area. The target is between 2 levels below and 5 levels above you.
2. Kill the monster. The item goes straight into your **green quest pouch** (*"You quickly pick up the..."*). If you've lost the pouch, a new one appears. Leave the item in the pouch.
3. Return to either of them and type `aquest` again. He takes the item from your pouch, you level up on the spot, and you receive a quest pill. If you don't have the item yet, he just tells you the quest isn't complete.

`score` reminds you of the item, monster and area while you're on a level quest.

---

## 12. Death and recovery

- You become a **spirit** right where you fell, with your spells stripped and your pet gone. A spirit can't fight, pick things up, practise or train, but `recall` always works for one. Anything floating near you drops to the floor there.
- **Your corpse, with all your gear in it, is moved to the morgue for you**: the City Morgue (`e` from the temple) from level 10, or the Mud School Morgue below level 10. There's no corpse run. Go there and type `enter corpse`. That puts you back in your body with everything it carried, coins included. (`get all corpse` doesn't work while you're a spirit.)
- Player corpses decay after 25–40 ticks (very roughly 25–60 minutes). If yours decays first, you get a new body, but **everything it held spills onto the morgue floor** where anyone can take it, so get there promptly.
- **Experience penalty:** you lose about **five-sixths of your progress toward the next level**. You can't lose a level, and nothing is lost if you'd made no progress. While you're on a level quest, death costs no experience.
- Your group and followers are unaffected.

---

## 13. Money, banks and shopping

- **Coins:** 1 platinum = 100 gold = 10,000 silver. Auto-gold collects coins from kills, and `worth` shows what you're carrying (not your bank balance).
- **Banks** keep game-time business hours (`time` shows the game hour):

| Bank | Location | Hours (game time) |
|---|---|---|
| First National Bank of Midgaard | `2s 3w 2n 2e s` | 8:00–20:00 |
| New Thalos Savings and Trust | in New Thalos | 7:00–19:00 |
| Ofcol City Depository | Ofcol | 9:00–20:00 |
| Southern Thera Savings and Loan | StoneBow Dale | 8:00–16:00 |
| First National Bank of Thera | Aerial City | 5:00–21:00 |

`deposit <amount>` and `withdraw <amount>` work in platinum, **in multiples of 10**. Each withdrawal costs a 2% fee, taken from what's left in the account, and each bank holds at most 30,000 platinum per player. Each bank keeps its own account. If you join a PK clan and get killed, your killer may get a passbook for one of your accounts (`help rob`); any deposit or withdrawal, even of 0, invalidates it.

- **Selling:** `value <item>` asks a shopkeeper for a price and `sell <item>` sells it. Shops only buy the kinds of items they sell.
- **Buying several:** `buy 5*pie`; `buy 2.sword` buys the second sword in the list.
- **Gems** (Jeweller, `2s e s`) are a light way to carry wealth.

---

## 14. Getting around: boats, flying, mazes and maps

### 14.1 Water and air

- **Deep water** rooms need a boat in your inventory (a **raft or canoe** from the captain, `3s 2e s`) or flying.
- **Air** rooms need flying: a **potion of flying** from the apothecary (`3s 3e n`) or the *fly* spell. Pixies, draconians, cloud giants, demons and gold dragons fly permanently.
- Areas reached through deep water: Sands of Sorrow, Mega City One, Pyramid, Elvandar, Dark Continent, Freeport and the 36 Chambers. Through air: In the Air, the Astral Plane, Aarakocran City and Aerial City.

### 14.2 Finding your way

- `exits` lists exits; auto-exit shows them every time you enter a room. Exits in parentheses, such as `(South)`, are closed doors: `open south`.
- `route all` is the game's own directions command. Its directions start from **Market Square** (`2s` from the temple) and cover a handful of areas and the New Thalos guilds.
- Your starting **maps** (`read map`, or `look map`) and the maps sold at Melancholy's (`3s w n`) show city layouts.
- `areas` lists every area. `where` shows players (or, with a name, a monster) in your current area.
- `run <direction>` sprints a random number of rooms in one direction for 50% more movement. It's handy on long straight roads, but it won't stop at an exact room.
- **Mind your movement points.** A new character has about 100 movement, and each step costs about 2 in town or on fields, 3 in forest, 4 in hills or shallow water, 6 in mountains or desert and 10 in the air. Flying or haste halves this. **Several routes in [section 9](#9-the-levelling-roadmap-where-to-go-levels-1-to-101) are longer than a new character can walk in one go**, and you'll see *"You are too exhausted."* Stop and `rest` (or `sleep`) partway, buy *refresh* from a healer, or spend a training session or two on `train move` (+10 each).

### 14.3 Mazes

Several areas contain **mazes whose exits reshuffle every time the area resets**, so no fixed directions work:

- **The Shadow Grove** (High Tower), which is the only way to Dragon Tower, Galaxy, Divided Souls, Dylan's Area and Redferne's
- The damp hallways in **Gnome Village**
- The Void at **Old Thalos**
- The confusing corridors of **Aarakocran City**
- The mini-maze in **Day Care**
- Parts of **Crystalmir Lake**

To get through one: enter, `look`, try exits methodically, and accept that you'll loop a few times. Don't rely on someone else's directions; they changed at the last reset.

---

## 15. Other players: channels, groups, clans and PK

- **Newbie channel limits:** `ooc` (or `.`) is open from **level 1** and reaches everyone in the game, so ask there if you're stuck. Until **level 10**, `tell`, `reply`, `gtell` and the other global channels are restricted. At level 10 you get the message *"You now have full channel permissions."* `say` (or `'`) always works in the same room. `help` and the `rules` are your friends.
- **Channels:** `ooc` (`.`), `ask`/`answer`, `grats`, `auction`, `music`, `quote`, `shout` (everyone, with a delay), `yell` (your area), `tell <player>`, `reply`. Type a channel's name alone to turn it off. `forget <player>` ignores someone.
- **Grouping:** `follow <leader>`, then the leader types `group <you>`. Members must be **within 14 levels** of each other. Grouped players share experience, auto-assist each other and can `gtell` (`;`). Auto-split shares coins. Don't kill-steal: attacking a monster someone else is fighting breaks the rules.
- **Notes:** `note list`, `note read`, and `unread` to see what's waiting. The `news` and `changes` boards carry announcements.
- **Clans and player-killing:**
  - **If you're not in a clan, other players can't attack or steal from you, and you can't attack them.** Player-killing is only between clan members, within 10 levels of each other.
  - First-tier characters can join a clan from **level 25 to 70** (second tier from level 15), by invitation from the clan's leader (`member accept`). Clan leaders are appointed by the immortals.
  - **PK clans only take Veterans.** `enlist` (level 12+) makes you a Recruit, open to player killing; five player kills or five deaths at other players' hands (arena fights don't count) promote you to Veteran. Non-PK clans don't need this.
  - A Veteran can instead declare themselves a **loner** (`loner`, from level 25, or 15 for higher tiers), which makes you player-killable without joining a clan.
  - Current clans: **Guardians** and **Judges** don't allow PK; **Dark Mist**, **Midnight** and **Angels** do. `clan list` and `help <clanname>` give details, and `help clanrules` explains the clan rules.
  - Clan members recall to their clan hall.
- **Arena duels:** `challenge <player>` starts a consensual fight in the Haunted House arena (`accept` / `decline`), when the staff have the arena open. `bet` lets spectators wager. Your `score` tracks arena wins and losses.
- **Rules summary** (`rules`): no multi-playing, no kill-stealing, no exploiting bugs (report them with `bug`), keep public language clean, and don't ask immortals to help you level.

---

## 16. Hero and beyond: tiers, advance and reroll

- **Level 101 is Hero**, the top mortal level. Levels 102 and up are immortal staff.
- **Second tier:** a Hero can `advance <newname>` once to create a **new character** in the second tier, which keeps your password. Second-tier classes are much stronger, and you may pick any of them (a mage doesn't have to become a wizard): **wizard, priest, mercenary, gladiator, strider, sage, lich, barbarian, knight**.
- **Third tier** characters are multi-class: a second-tier primary plus a first-tier secondary class, with access to both classes' skills. The quest shop mentions `quest buy reroll` for third-tier Heroes.
- **`reroll`** (type it twice) sends your current character back through creation at level 1 in its **current** tier, with newbie gear. It's different from `delete`, which erases the character entirely (also typed twice).
- Higher tiers start with more training sessions and practices, but earn a little less experience per kill.

---

## 17. Quick reference card

```
MOVE        n e s w u d   run <dir>   exits   scan   where   recall (/)   open <dir>
            guide <area>   (directions to any area from where you stand)
LOOK        look  look <thing>  examine <corpse>  consider <mob>  score  affects  worth
FIGHT       kill <mob>  flee  wimpy  rescue <ally>  stance <x>  autostance <x>  mock <mob>
MAGIC       cast '<spell>' <target>   spells   skills   quaff  recite  zap  brandish
GEAR        inventory  equipment  wear  wield  second  hold  remove  compare  lore
            get all corpse   get <x> <container>   put <x> <container>   sacrifice  donate
GROW        practice  train  gain list   (all at the Dungeonmaster: 2s from the temple)
QUEST       quest request|info|time|complete|list|buy   (Dungeonmaster, 2s)
            aquest   (Heimdall n 3u or Dungeonmaster 2s; from level 5; level quests at 50 and 100)
MONEY       list  buy  sell  value   deposit/withdraw (multiples of 10 platinum)
TALK        say (')  tell  reply  gtell (;)  ooc (.)  note  unread
SETTINGS    scroll 0  prompt  colour  autolist  brief  compact  wimpy
HELP        help <topic>   commands   rules   areas   route all   class <name> skill
```

**From the Temple of Thoth:** altar healer `n` · Heimdall `n 3u` · morgue `e` · donations `w` · fountain `s` · **Dungeonmaster `2s`** · forger `s e n` · potions `3s 3e n` · boats `3s 2e s` · bank `2s 3w 2n 2e s` · armour `2s w s` · weapons `2s 2e n` · Mud School `7s w u` · New Thalos `2s 15e`.

**The first-session checklist:**

1. `scroll 0`, then unpack and wear the survival pack ([4.2](#42-unpack-the-survival-pack-dont-skip-this)).
2. Spend your 30 trains and 35 practices ([4.3](#43-spend-your-30-trains-and-35-practices-now)).
3. `autostance bull` (or another stance) and `wimpy`.
4. Clear the Mud School cages and Arena. Their high internal levels and the under-11 bonus make them worth far more experience than their hit points suggest.
5. Walk to town (`d e 7n`), then go to Smurfville (`2s 7e n`) and the Shire (`2s 5w n`). Once you have 35 gold, buy sanctuary from Thoth's priest (`2s 3e 3n w s`, `repent sanctuary`) before a hard fight.
6. At level 5, take autoquests from Heimdall (`n 3u`). Take Dungeonmaster quests (`2s`) whenever they're available.
7. Use your first platinum at the forger (`s e n`).
