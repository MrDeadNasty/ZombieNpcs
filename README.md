# ZombieNpcs
Turns a portion of the map's NPCs into shambling zombie-like threats while survivor NPCs fight back using full ASO AI behaviour (see ReadMe for ASO).

ZOMBIE NPCs
 
  Each zombie:
  - Staggers side-to-side as it walks, weaving with a slow lurch
  - Grunts and vocalises at random intervals (add your own audio files)
  - Has terrible aim with extra angular spread on every shot
  - Hesitates before firing — slow to pull the trigger
  - Moves slower than a normal NPC
  - Can be given a health multiplier to make them tankier
  - (if possible) Is disarmed of ranged weapons and given melee only (knife) or accuracy/spread for weapons if melee not possible.
 
NPC FIGHTERS
  
  A separate pool of normal NPCs is tagged as fighters and given ASO's full
  AI brain. They will:
 
  - Detect zombies using ASO's graduated detection meter (affected by weather,
    time of day, distance, movement speed, and attachments)
  - React with faction-appropriate delay before engaging
  - Use cover, flanking, suppression fire, and tactical decision-making
  - Track ammo and perform tactical or emergency reloads
  - Switch to full-auto at close range
  - Have a personality (cautious / balanced / aggressive) rolled on spawn
 
  Fighters will also fight the player and other hostile factions as normal —
  the zombie threat is layered on top of the existing ASO faction war.
 
 
--------------------------------------------------------------------------------
  REQUIREMENTS — READ CAREFULLY
--------------------------------------------------------------------------------
 
  Metro Mod Loader v3.1+
  
   https://modworkshop.net/mod/55623
    Required. The mod will not load without it.
 
  Mod Configuration Menu (MCM) by DoinkOink
  
   https://modworkshop.net/mod/53713
    Recommended. Without it all settings use defaults and must be edited
    manually in the config file (see MANUAL CONFIG below).
 
  *** ASO — Armed Enhancement: AI System Overhaul by Skuddster ***
  
   https://modworkshop.net/mod/56583
    REQUIRED for NPC fighters. Without ASO the fighter NPCs will still
    spawn and move around, but they will not have enhanced detection,
    faction targeting, reaction time, personality, ammo tracking, or
    suppression fire. The mod will print a warning in the output log if
    ASO is not detected at startup.
 
 
--------------------------------------------------------------------------------
  INSTALLATION
--------------------------------------------------------------------------------
 
  1. Install Metro Mod Loader (follow its own instructions).
  2. Install MCM — set its priority to -100 in the launcher so it loads first.
  3. Install ASO — leave its priority at the default (60).
  4. Drop ZombieNPCs.vmz into:
       Steam\steamapps\common\Road to Vostok\mods\
  5. Launch the game. The Metro pre-launcher appears.
  6. Tick: MCM, ASO, Zombie NPCs.
     Load order should be:  MCM (-100)  →  ASO (60)  →  Zombie NPCs (70)
     The priority numbers handle this automatically.
  7. Hit Launch. Open Settings → MCM → Zombie NPCs to configure.
 
 
--------------------------------------------------------------------------------
  CONFIGURATION  (Settings → MCM → Zombie NPCs)
--------------------------------------------------------------------------------
 
  GENERAL
    Mod Enabled ............. Master on/off switch. Default: ON
    Debug Logging ........... Prints detailed info to the output log. Default: OFF
 
  ZOMBIE SPAWN
    Min Zombies ............. Floor — mod keeps at least this many zombies alive.
                              Default: 3  |  Range: 0–50
    Max Zombies ............. Hard cap on simultaneous zombie NPCs.
                              Default: 7  |  Range: 0–50
    Zombie Spawn Timer Min .. Minimum seconds between zombie top-up checks.
                              Default: 5s  |  Range: 1–120s
    Zombie Spawn Timer Max .. Maximum seconds between zombie top-up checks.
                              Default: 15s  |  Range: 1–120s
    Zombie Health Multiplier  Multiplies zombie base health. 2.0 = twice as tough.
                              Default: 1.0  |  Range: 0.25–5.0
 
  NPC FIGHTERS  (requires ASO)
    NPCs Fight Zombies ...... Master toggle for the fighter pool. Default: ON
    Min NPC Fighters ........ Floor — keeps at least this many fighters alive.
                              Default: 2  |  Range: 0–50
    Max NPC Fighters ........ Hard cap on simultaneous fighter NPCs.
                              Default: 5  |  Range: 0–50
    NPC Spawn Timer Min ..... Minimum seconds between fighter top-up checks.
                              Default: 8s  |  Range: 1–120s
    NPC Spawn Timer Max ..... Maximum seconds between fighter top-up checks.
                              Default: 20s  |  Range: 1–120s
 
  ZOMBIE BEHAVIOUR
    Stagger Strength ........ Side-to-side sway amplitude. 0 = none, 1 = extreme.
                              Default: 0.35  |  Range: 0–1
    Stagger Speed ........... Oscillation frequency. 0 = very slow, 1 = fast.
                              Default: 0.45  |  Range: 0–1
    Grunt Interval Min ...... Minimum seconds between zombie vocalisations.
                              Default: 4s  |  Range: 0.5–30s
    Grunt Interval Max ...... Maximum seconds between zombie vocalisations.
                              Default: 10s  |  Range: 1–60s
    Zombie Aim Spread ....... Extra angular error on zombie shots (degrees).
                              Default: 18°  |  Range: 0–45°
    Zombie Fire Delay ....... Extra seconds zombie waits before shooting.
                              Default: 1.2s  |  Range: 0–5s
 
 
--------------------------------------------------------------------------------
  MANUAL CONFIG  (without MCM)
--------------------------------------------------------------------------------
 
  Edit the config file directly at:
    %APPDATA%\Road to Vostok\MCM\ZombieNPCs\config.ini
 
  The file is created on first launch. All settings are stored as dictionaries
  with a "value" key — change the value field only, leave the rest alone.
 
  Example:
    [Int]
    min_zombies={"name":"Min Zombies","value":5, ...}
                                             ^ change this number
 
 
--------------------------------------------------------------------------------
  ADDING GRUNT SOUNDS
--------------------------------------------------------------------------------
 
  The mod has audio slots ready. To use them:
 
  1. Place OGG or WAV files inside the .vmz (rename to .zip, add files, rename
     back to .vmz) at:
       mods/ZombieMod/audio/grunt1.ogg
       mods/ZombieMod/audio/grunt2.ogg
       mods/ZombieMod/audio/grunt3.ogg
 
  2. Open mods/ZombieMod/AIHooks.gd and uncomment the lines in the
     GRUNT_SOUNDS constant at the top of the file:
       const GRUNT_SOUNDS = [
           "res://mods/ZombieMod/audio/grunt1.ogg",
           ...
       ]
 
  Sounds are played at 3D world position with logarithmic falloff. They
  are pitch-shifted slightly each time so repeated clips don't sound
  mechanical.
 
 
--------------------------------------------------------------------------------
  COMPATIBILITY
--------------------------------------------------------------------------------
 
  Works alongside FactionWarfare + More Enemies (ModWorkshop 56026).
  Works alongside ASO (required for fighter AI — see above).
  No known conflicts with other mods that don't touch AI.gd or AISpawner.gd.
 
  If you use another mod that also hooks AI.gd or AISpawner.gd, load order
  may matter — set priorities in the Metro pre-launcher accordingly.
 
 
--------------------------------------------------------------------------------
  KNOWN LIMITATIONS
--------------------------------------------------------------------------------
 
  - Grunt audio is silent until you add OGG files (see ADDING GRUNT SOUNDS).
  - Melee loadout requires the NPC's scene to include a melee weapon slot.
    If a zombie NPC has no melee weapon in its loadout, it keeps its ranged
    weapon. A debug log message will appear if this happens.
  - Fighter NPC AI quality depends entirely on ASO being installed. Without
    ASO they patrol normally but do not actively hunt zombies.
  - Zombie health multiplier only applies if the NPC node exposes a health
    property — most standard NPCs do. Boss-type NPCs may behave differently.
 --------------------------------------------------------------------------------
  CREDITS
--------------------------------------------------------------------------------
 
  Zombie NPCs mod — built from scratch using:
   - Metro Mod Loader hook API (ametrocavich/tetrohydroc)
    
   - MCM integration (Mod Configuration Menu, Doink Oink)
    
   - (Optional Depencendy) Fighter AI via ASO (Armed Enhancement - AI System Overhaul, Peter Master)
--------------------------------------------------------------------------------

[mod info]
name="Zombie NPCs"
id="zombie-npcs"
version="4.0.0"
description="Turns NPCs into shambling zombies. Fighter NPCs use ASO (Armed Enhancement - AI System Overhaul) for full AI. Requires ASO."
author="DeadNasty/Claude"
priority=70
 
[autoload]
ZombieModConfig="res://mods/ZombieMod/Config.gd"
ZombieModMain="res://mods/ZombieMod/Main.gd"
 
[hooks]
"res://Scripts/AI.gd" = "Activate, Parameters, SelectWeapon"
"res://Scripts/AISpawner.gd" = "_ready, SpawnWanderer, SpawnGuard, SpawnHider, SpawnMinion, SpawnBoss"
