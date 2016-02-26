# mageBotSettings.ini #

The mageBotSettings.ini is the heart of the mageBot.mac.  Without it the macro will not run correctly.  At the same time if it is not set up correctly the macro can do some very quirky things.  This page will explain what each setting in the ini is for and give some examples of how to use it.

## [General](General.md) ##

| **Setting** | **Type** | **Description** |
|:------------|:---------|:----------------|
| SpellCoolDown | _timer_  | This specifies the global cooldown time between spell casts.  Not necessarily the eq spell cooldown time, but how long you want the mage to wait between each spell cast. |
| SitAt       | _integer_ | This is the percent health your target has to be at before the mage will sit during combat to med. |
| MinMobLvl   | _integer_ | The minimum level of a mob that the mage will engage in combat with, unless the mob attacks the mage |
| MaxMobLvl   | _integer_ | The maximum level of a mob that the mage will engage in combat with, unless the mob attacks the mage |
| MobRadius   | _integer_ | The maximum distance a mob can do for the mage to attack it |
| PetHeal     | _string_ | The name of the pet heal spell to use when healing the pet |
| PetHealPct  | _integer_ | The percent health of your pet when you want to start healing it |
| PetHealTo   | _integer_ | The percent health of your pet to stop healing it. |
| MinSafeDistance | _integer_ | The minimum distance the mage should be from mobs.  Its best to have this slightly higher than the mobs melee range that you are botting near. |
| ResistTries | _integer_ | The number of times to try casting a spell if you are resisted |
| MinRestMana | _integer_ | The percent mana that you will stop to med at |
| MinRestToMana | _integer_ | The percent mana that you will med to once you have stopped to med |
| MinRestOverHPs | _integer_ | The percent health that you will stop to recover health at |
| TimeToSitAfterCast | _timer_  | The amount of time to wait after casting a spell before you sit |
| CircuitRestTime | _timer_  | Once you run a full circuit (your complete path) this is the amount of time the mage will stop to rest, mainly used for giving mobs time to respawn on your path |
| ReplyToTells | _boolean_ | Sets wether or not the mage will respond to tell commands sent to her.  In any situation it will never respond to a tell from a pc that is not on your SafePCs list |
| WalkPath    | _boolean_ | If set to false the mage will stand at the starting point and only use the path to get out of range of a mob.  Usefull if your just camping a named mob. |
| PathName    | _string_ | Specifies the name of the path to use.  default will tell it to use the default path name which is ${Zone.ShortName} |
| LootCorpses | _boolean_ | Specifies wether the mage will loot corpses or not |
| LootReturnNearestLoc | _boolean_ | If set to true the mage will return to the nearest loc after looting a corpse, instead of the loc it was at when the mob died |


## [GroupSettings](GroupSettings.md) ##

| **Setting** | **Type** | **Description** |
|:------------|:---------|:----------------|
| GroupMode   | _boolean_ | If set to true the macro does not require a path to run.  It will instead stay at its starting location and assist the MainAssist at the specified assist percentage. |
| MainAssist  | _string_ | The name of the player to assist for the target to attack |
| PetAssistPct | _integer_ | The percentage when you attack with your pet.  Also will not cast any spells until the pet is engaged |
| GroupBuffAtStart | _boolean_ | Specifies wether the mage should do groupbuffs when the macro is started, if set to false you can make the mage group buff by sending a tell saying groupbuff |
| MinBuffCheckTime | _timer_  | The amount of time between buff checks, keeps the mage from constantly cycling through targets while not fighting. |

[SelfBuffs](SelfBuffs.md)
Value=4
SelfBuffName1=Eidolic Guardian Rk. II
SelfBuffName2=Shield of the Void
SelfBuffName3=Prime Symbiosis
SelfBuffName4=Ornate Runed Totem Staff
SelfBuffName5=NULL
SelfBuffText1=Eidolic Guardian Rk. II
SelfBuffText2=Shield of the Void
SelfBuffText3=Prime Symbiosis Recourse
SelfBuffText4=Maelin's Meditation
SelfBuffText5=NULL
SelfBuffSlot1=gem9
SelfBuffSlot2=gem9
SelfBuffSlot3=gem9
SelfBuffSlot4=item
SelfBuffSlot5=gem9
[PetBuffs](PetBuffs.md)
Value=3
PetBuffName1=Brimstoneskin
PetBuffName2=Burnout VIII
PetBuffName3=Iceflame Tenement
PetBuffName4=NULL
PetBuffName5=NULL
PetBuffText1=Brimstoneskin
PetBuffText2=Burnout VIII
PetBuffText3=Iceflame Tenement
PetBuffText4=NULL
PetBuffText5=NULL
PetBuffSlot1=gem8
PetBuffSlot2=gem8
PetBuffSlot3=gem8
PetBuffSlot4=gem8
PetBuffSlot5=gem8
[GroupBuffs](GroupBuffs.md)
Value=1
GroupBuffName1=Lavaskin Rk. II
GroupBuffDisplayName1=Lavaskin Rk. II
GroupBuffAlias1=ds
GroupBuffClass1=WAR|SHD|PAL|RNG|MNK|ROG|BRD|BST|BER|SHM|CLR|DRU|WIZ|MAG|ENC|NEC
GroupBuffSlot1=gem7
[SafePCs](SafePCs.md)
Value=0
PCName1=NULL
[WantedLoot](WantedLoot.md)
Value=0
LootItem1=
[DestroyLoot](DestroyLoot.md)
DestroyUnknown=false
Value=0
LootItem1=
[IgnoreMobs](IgnoreMobs.md)
Value=0
MobName1=Gillamina
MobName2=dead
[Combat](Combat.md)
Value=6
SpellName1=Rancorous Servant
SpellSlot1=gem6
SpellMaxMobs1=100
SpellMinMobs1=1
SpellMaxMobHPs1=100
SpellMinMobHPs1=30
SpellMinMana1=20
SpellRecastDelay1=18s
SpellCondition1=Me.Song[of Exquisite Radiant Mana](Gift.md).ID

SpellName2=Bolt of Molten Scoria
SpellSlot2=gem10
SpellMaxMobs2=100
SpellMinMobs2=1
SpellMaxMobHPs2=80
SpellMinMobHPs2=40
SpellMinMana2=30
SpellRecastDelay2=5s
SpellCondition2=Me.Song[of Power](Flames.md).ID

SpellName3=Torrent of Thunderbolts Rk. II
SpellSlot3=gem4
SpellMaxMobs3=1
SpellMinMobs3=1
SpellMaxMobHPs3=90
SpellMinMobHPs3=21
SpellMinMana3=20
SpellRecastDelay3=15s

SpellName4=Fickle Pyroclasm
SpellSlot4=gem2
SpellMaxMobs4=100
SpellMinMobs4=1
SpellMaxMobHPs4=92
SpellMinMobHPs4=21
SpellMinMana4=10
SpellRecastDelay4=10s

SpellName5=Shock of Cineral Steel Rk. II
SpellSlot5=gem5
SpellMaxMobs5=100
SpellMinMobs5=1
SpellMaxMobHPs5=85
SpellMinMobHPs5=5
SpellMinMana5=10
SpellRecastDelay5=10s

SpellName6=Malosenea
SpellSlot6=gem7
SpellMaxMobs6=100
SpellMinMobs6=1
SpellMaxMobHPs6=100
SpellMinMobHPs6=50
SpellMinMana6=15
SpellRecastDelay6=5m

[Alerts](Alerts.md)
AlertDeathAudioFile=null
Value=0
AlertMobName1=null
AlertAudioFile1=null