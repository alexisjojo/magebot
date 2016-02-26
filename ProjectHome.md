Fully automated, run solo on a pre recorded path or in group mode assiting and doing extra dps.


---

# devCommon V1.61 - 02/08/2009 Updates #

Files Changed
devCommon.inc v1.61

Bug Fixes
-Corrected a typo in the new global follow command that was preventing follow from working.

New Additions
-

Additional Notes
The new 1.61 is included in the rar download but is also available for download by it self if you've already download the rar.
 _# mageBot V2.9 - 02/08/2009 Updates #_

Files Changed
mageBot.mac
devCommon.inc v1.6
devMovement.inc v1.5
mageBotSettings.ini

Bug Fixes
-Corrected a bug causing TimeToSitAfterCast setting to be ignored.
-Added a delay when checking group buffs that should help with the rebuffing when not necessary problem that some people have noticed.

New Additions
-Modifed for devCommon.inc v1.6
-Echo messages are now colorful if you have the MQ2CEcho plugin.
-Added new OutOfCombatSit setting, see ini changes for details.
-More information is logged to help when trying to track down problems.
-Mobs on your ingore list should no longer even be targeted unless they are detected as adds.
-Now when running in groupmode, if a mob is inside of your minsafedistance but not facing you the mage will not sit but will still cast spells. If they are facing you and is in minsafedistance the mage will not cast spells.
-Added a new spelltype grouping system. Some people were having problems with some spells not casting further down the spell list. What you would have to do is reorganize your spell list to make sure conditional or long lasting spells always came first in the list. With this type grouping this is no longer necessary. You will be able to create spell types that cast in the specified order, and then assign your spells to a specific type so that it will cast with that group. **NOTE** this is completely optional, if you do not wish to use this spell casting will work like it always has, and you do not even need to even change your INIs. See ini changes for full details.

INI Changes
-New INI Setting [GroupSettings](GroupSettings.md) OutOfCombatSit, True or False value, specifies wether the mage will sit when out of combat in groupmode if it does not need to in order to med. The mage will still sit when it needs to med out of combat.
-New INI Settings

Code:
[Combat](Combat.md)
SpellSetTypeValue=0
SpellSetType1=NULLThis will enable you to create custom spelltypes that can be assigned to each spell (see spell ini entries further down for info on this). When the mage is looking for a spell to cast it will check by group starting with SpellSetType1. It will still cast all spells not assigned a type after check all the Types. If you do not wish to use this you do not need to make any changes.

Example:

Code:
[Combat](Combat.md)
SpellSetTypeValue=1
SpellSetType1=Special

Value=3
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
SpellType3=SpecialIn this example, even though Torrent of Thunderbolts is the 3rd spell it would get checked first when the mage looks for a spell that is ready to be cast and the situation meets all requirements. This is mainly just a way to make sure your long use or conditional spells / alt abilities / items gets used even if you have them further down the spell list, without needing to reorganize your entire list.

-Spell entry INI Additions, now on each spell entry you can use SpellMaxHPs and SpellType. SpellType is explained above, SpellMaxHPs will simply make it so you must be below that amount of hitpoints to cast the spell. Not really all that usefull as a mage but I made some changes to the common file and this was in my skBot so the mageBot can take advantage of it now as well if you find a need for it.

# devCommon V1.6 - 02/08/2009 Updates #

Files Changed
devCommon.inc v1.6

Bug Fixes
-Added checks to prevent using interrupt if you are on a mount. Should not dismount you anymore, but spells will finish casting even if a mob dies.
-Fixed a bug with assisting in groupmode that could cause you to get stuck on a corpse.
-Fixed a bug with CorpseCheck routine that could cause you to have an invalid number of live targets, causing spells that required certian numbers of live targets to be cast incorrectly.
-Fixed a bug in StripText routine that was not always stripping all escape characters.

New Additions
-The CheckForAggro routine now does a better job of testing if a mob is actually aggro on you.
-SendTell routine will now strip any escape characters from a message before it is sent "\a"
-Added a variable defaultEchoColor that sets the default echo output color
-Added more checks that should make sure the character will continue to fight if the main assist is not present or dead.
-buffCheck(bool useTimer) routine moved to devCommon.inc
-A lot of reused variables in my bots have been moved to devCommon.inc instead of being declared in each macro. This also gives more options of adding features to all my bots in the future.
-Added GlobalCommands(string comFrom,string comText) routine. This will contain commands that can be used for any bot of mine. (These commands can be issued in a tell from a SafePC or in an /echo on the character). Currently available global commands (note some of these were available before but were moved to here):
safepc 

&lt;name&gt;

 - adds or removes a safepc, this will update in the ini as well.
gnoremob 

&lt;name&gt;

 - adds or removes an ignored mob, this will update in the ini as well.
follow 

&lt;target&gt;

 - makes the character followed the specified target.
stay - sets the characters home location to their present location and turns off follow.
docmd 

&lt;command&gt;

 - can make the character do any command. It does not work with any ' or " in the command though. Example: /tell bot docmd /pet hold - the bot will do the /pet hold command.
-Created a new CommonLoad routine. If you use my common file for other macros you'd want to /call CommonInit before you load any settings or declare any variables. Once you have all your settings loaded CommonLoad will finish loading with any settings you loaded that it uses.
-The devCommon.incnow has a built in verification system to make sure the bot you are using is of sufficient version to be compatible. If it is not a warning message will be displayed and the macro will be ended.
-There is now and Ignored mobs alert list, and a safe pc alert list created. By default the numbers are 101 for ignore mobs and 102 for safe pcs. If you wish to change this add a /varset alertList n for ignore mobs or a /varset safeAlertList n for safepcs before calling CommonLoad. This should make it so none of my bots ever target an ignored mob, and make safepc checks a little quicker.

Additional Notes
Not all of these updates apply specifically to all my bots currently, some are really only used in the mage or the sk but not both. But I'm including them in the update notes for the devCommon to have one universal set of notes for this file.

# devMovement V1.5- 02/08/2009 Updates #

Files Changed
devMovement.inc v1.5

Bug Fixes
-No bug fixes

New Additions
-Movement routins now return more information about the movement success or failure. Also if rooted the movement routine will exit now instead of sitting around waiting for root to wear off and preventing bots from doing anything else while watiing.

Additional Notes
Not all of these updates apply specifically to all my bots currently, some are really only used in the mage or the sk but not both. But I'm including them in the update notes for the devMovement to have one universal set of notes for this file.

Additional download notes
My other bots are NOT compatible with this release of devCommon.inc. If you use any of my other bots you must download new versions that are compatible with this version of devCommon.inc.


# Magebot V2.8 - 1/30/2009 Updates #
Additional Notes
I realize the patch notes below are not in a very pretty format like I normally do, but I wanted to get the update posted here tonight and didnt have time to sift through all the update notes to make them pretty. I'll work on this within the next few days. But the download is there, just make sure you look at the example ini included in the download for new ini items.



mageBot V2.8 - 01/30/2009 Updates

Files Changed
mageBot.mac
devCommon.inc v1.5
devMovement.inc v1.4
mageBotSettings.ini

Bug Fixes
-Fixed some bugs related to the follow command and all around improved follow. The mage should now properly follow the specified target, if combat is encountered while following it will disengage follow and act as usual in combat. When finished it will attempt to refollow the specified follow target. Note follow mode is for gorupmode only.

New Additions
-You can now modify unsafePCAction for solo mode, see ini changes and devCommon update notes for full details.
-AlertUnsafePC added, see ini changes for details
-Made a few improvements to combat while in groupmode. You should notice less target swapping and all around improved performance.
-Added the ability to toggle camping after gating, see ini for full details.
-Added a check for groupmode to make the mage sit when out of combat and not in follow mode.

INI Changes
-New INI Item [General](General.md) UnsafePCAction. This will tell the bot what to do when running in solo mode and it encounters and unsafepc. Options are: Gate, Pause, Continue, Stop, Camp. Gate will be executed immediately, others will only be executed when the mage is out of combat. I highly recommend if your using the bot afk to set an AlertUnsafePC to play if you do not have the bot set to gate.

Also note, UnsafePCAction under [GroupSettings](GroupSettings.md) is still used for groupmode action. Default action for solo mode remains gate, for group mode pause.

-New INI item [Alerts](Alerts.md) AlertUnsafePC. Will play the specified sound file if an unsafepc is encountered, wether in groupmode or solo mode.
-New INI item [General](General.md) CampAfterGate. This is a true or false setting, if set to true (which is the default) it will camp after gating if it gates for any reason. If set to false it will not camp after gating.

devCommon V1.5 - 01/29/2009 Updates

Files Changed
devCommon.inc v1.5

Bug Fixes
-No bug fixes

New Additions
-Improved target selection for group mode.
-Added an alert to camp check subroutine, variable alertUnsafePC.
-Added support for using color echos with htw's MQ2CEcho plugin

Additional Notes
Not all of these updates apply specifically to all my bots currently, some are really only used in the mage or the sk but not both. But I'm including them in the update notes for the devCommon to have one universal set of notes for this file.

devMovement V1.4 - 01/29/2009 Updates

Files Changed
devMovement.inc v1.4

Bug Fixes
-No bug fixes

New Additions
-Made it so that you do not have to run in first person mode for doors to work. It will automatically change to first person mode if it thinks a door is encountered.

Additional Notes
Not all of these updates apply specifically to all my bots currently, some are really only used in the mage or the sk but not both. But I'm including them in the update notes for the devMovement to have one universal set of notes for this file.

mageBot V2.7 - 01/16/2009 Updates

Files Changed
mageBot.mac
devCommon.inc v1.4
devMovement.inc v1.3
mageBotSettings.ini

Bug Fixes
-Fixed a bug causing LootReturnNearestLoc setting to be ignored

New Additions
-Modified for devCommon.inc v1.4

INI Changes
-Added LeaveUnknown setting to LeaveLoot section. This will take priority over DestroyUnknown. This will leave any loot, that does not have a setting, on the corpse if set to true.

devCommon V1.4 - 01/16/2009 Updates

Files Changed
devCommon.inc v1.4

Bug Fixes
-Corrected a bug that was causing items to not be cast correctly if used as a combat spell.
-Corrected a problem with casting cool down timers not being applied correctly under some circumstances.
-Corrected a potential problem in the evac routine that could cause it not to work properly.

New Additions
-Added a new itemswapcheck routine that will check if the item cannot be swapped automatically when attempting to cast it. (Example: You need to cast a must equip shield but have a 2hander equipped)
-Changed looting subroutine to allow for a leaveUnknown boolean to leave itemson a corpse that have no found loot setting.
-Choosetarget routine should now put healer type mobs higher on the priority list

Additional Notes
Not all of these updates apply specifically to all my bots currently, some are really only used in the mage or the sk but not both. But I'm including them in the update notes for the devCommon to have one universal set of notes for this file.

Special thanks goes out to Shank for helping me with getting the itemswap and item casting fixed

devMovement V1.3 - 01/16/2009 Updates

Files Changed
devMovement.inc v1.3

Bug Fixes
-Fixed a problem with MoveToSpawn routine that could cause it to not recognize being stuck.
-Made a few other stuck detection modifications to better detect when stuck.

New Additions
-SetNearestLoc routine now attempts to only set a nearby loc that is near your position on the path. This is to avoid skipping large sections of your path because of overlapping sections.
-All movement routines will now attempt to recognize when near a door and facing it and open it. This will only work if you run in first person mode, but should enable you to be able to create paths that go through doors.

Additional Notes
Not all of these updates apply specifically to all my bots currently, some are really only used in the mage or the sk but not both. But I'm including them in the update notes for the devMovement to have one universal set of notes for this file.

Magebot V2.6 - 01/07/2009 Updates

Files Changed
mageBot.mac
devCommon.inc v1.2
devMovement.inc v1.2

Bug Fixes
-Fixed stuck detection problems with the new detection in v2.5

New Additions
-A few minor code improvements here and there, nothing really changed though.

Magebot V2.5 - 01/04/2009 Updates

Files Changed
mageBot.mac
pathRecord.mac
**NEWFILE** devMovement.inc v1.1
**NEWFILE** devCommon.inc v1.1
**NEWFILE** pathZUpdate.mac
**OBSOLETE** mageBotMovement.inc

Bug Fixes
-None, although I may have created more in this version! hehe

New Additions
-Modified for new include files
-If you have a buff like a mount that can only be used outdoors and it tries to use it indoors, it should recognize it and remove the buff from the buff list for the duration of the run.
-Z axis support on paths. All old paths should still run without a problem, all new paths recorded with my pathRecord.mac will include a z axis component. If you would like to add z axis support to one of your old paths, run the path using pathZUpdate 

&lt;pathname&gt;

 (or leave blank for default)

Just stand near the beginning of the path and run the macro and it will walk it and update the z axis. I recommend using /stealth on while doing this so that you do not get attacked.). If for some reason something messes up while you are updating the z axis, run this command /macro pathzupdate 

&lt;pathname&gt;

 true (again default for 

&lt;pathname&gt;

 to use the default path int he zone). This command will clear all z axis components from the specified path. I highly recommend backing up your path.ini before using pathzupdate.mac. I did my best bo make sure there were no errors in it, but you never know!

This is very usefull in areas where you may be falling off the side of a cliff and getting stuck, or if your path crosses itself at a different height on the map. This also should add support for underwater paths, although I have not tested it.
-New stuck detection code. My new code relaxes some areas that were showing as stuck to easily while being more aggresive in others. Also if your path has z axis support it will detect if you fall off and cannot get back on your path.

Other Notes
Since I have a common file now that will be used in all my current and future bots, this file is subject to get updated without the bot itself being update. Both include files have an init sub routine (MovementInit and CommonInit) that I call when loading them that will echo the version number etc. In my update notes I will include the version number that the current bot version is supported to work with. I will make every effort to make sure if something is changed it either works with previous versions, or I will put an update for the bot out to work with it. This is so that those of you who may end up using more than one of my bots will not have any problems because of different include versions.

You are welcome to use these include files in your own macros if you like, but I do not have any write ups for the subroutines in these files yet.

Magebot V2.4 - 01/02/2009 Updates

Important Notes
This is my last major planned update. I now have everything functioning in the bot that I would like to have in it. This however does not mean I will no longer update the bot, I just have nothing further planned at this time. I will of course address bugs as fas as I can, and continue to take requests for changes or new additions. But as of right now, I plan to start working on my next bot (which is going to be an SK bot). Please continue to let me know of any problems you have or if you need help with anything!

Files Changed
mageBot.mac
mageBotSettings.ini

Bug Fixes
-Fixed it so when summoning items it now targets yourself so that mod rods will be summoned correctly.

New Additions
-Added the ability to wait for and accept rezzes in group mode.
-Added the ability to use mod rods and heal pots. (See ini changes)
-Added the ability to loot no drop items. (See ini changes)

INI Changes
-New INI Entries for mod rods and Heal pots, under [General](General.md)

Code:
ModRodName=Rod of Prime Transvergence |The name of the mod rod item
ModRodHPs=20 |The minimum pct of hitpoints to use a mod rod
ModRodMana=40 |The pct mana to use the mod rod at
HealPotName=Distillate of Celestial Healing XIII |The name of the heal pot
HealPotHPs=40 |The pct HPs to use the heal pot atIf you leave the names set to null then the items will not be used.
**Note** For mod rods, you still have to add an entry to summoned items for the mod rod to be summoned!

-New ini entry for looting no drop items under [LeaveLoot](LeaveLoot.md)

Code:
LootNoDrop=true |True or false for wether to allow looting of no drop itemsI put this under LeaveLoot because if you set it to false it will not attempt to loot and destroy it or keep it, but this setting will work for any. For example if you have it set to lootnodrop items, and then in destroyloot you have it set to destroy an o drop item, it will still destroy it, but if you have it set not to lootnodrop items it will not even loot it to destroy it, it will simply leave it on the corpse

Magebot V2.3b - 01/01/2009 Updates

Files Changed
mageBot.mac

Bug Fixes
-Fixed a bug that could cause pets not to engage properly in groupmode. It's really fixed this time!

New Additions
-Added a command assist 

&lt;target&gt;

 to change the main assist while the bot is running in groupmode. (Remember as of last update you can use /tell commands in /echo now as well!)
-Changed the way assist targeting works in groupmode to prevent the target from being cleared so much if your mainAssist is also the puller.

Magebot V2.3 - 12/29/2008 Updates

Files Changed
mageBot.mac
mageBotMovement.inc

Bug Fixes
-Fixed a bug that could cause pets not to engage properly.
-Fixed a bug causing the macro not to buff mercs.
-Fixed a bug that could cause the bot to forget all mobs as well as eventually lead to it getting stuck if repositioning around a mob caused you to get further away from the mob than minMobRadius setting.

New Additions
-Updated /tell commands and the helplist for it.
-Made it so that you can now /echo commands (/echo help for further information)

Magebot V2.2a - 12/17/2008 Updates

Files Changed
mageBot.mac

Bug Fixes
-Corrected a bug with pet focus not working correctly if you did not let the macro summon your pet
-Corrected a bug with LootLeave where it was not working on partial item names (it will now accept a partial name Ex: uncut for Uncut Jacinth)

New Additions
-Added LootAlerts. In each section dealing with loot in the ini you can add a line LootAlert

&lt;n&gt;

=<file location\name> You can use this to play audio files if that loot item is handled. 

&lt;n&gt;

 is the LootItem number. If left out or set to Null it will not play anything.

# Magebot V2.1 - 11/15/2008 Updates #

_There are a lot of ini changes in this update so your going to have to either make a lot of changes in your ini or restart a new one based off the example included in the rar file.  Sorry about this but it's for some good improvements and will hopefully be the last time so many changes are necessary._

## Files Changed ##
mageBotMovement.inc
mageBotSettings.ini
mageBot.mac

## Bug Fixes ##
  * Fixed a bug that came up if you have your mobRadius set higher than 75.  It would target a mob but then keep running unless you got within a radius of 75.
  * Tweaked the aggro check when casting spells some, in some cases it would start to cast spells and interuppt them because of a mob being to close, but then instead of attempting to reposition it would try to cast the spell again.
  * I have modifed the movement routine to try to avoid getting in a situation where you are stuck more.  It will now attempt to move to a locand if it cannot get there it will go back some and try to get to each loc on the path until it gets to the end.  If it gets to the end and still cannot get to any loc then it will assume it is stuck and gate out.  Also it will not continue to try and move if it is stunned or rooted (if you are using the fixed version of MQ2Debuffs)

## New Additions ##
  * Added a rampage check, you will no longer sit for the duration of a fight where a mob rampages the mage.
  * Added a summon check, if summoned instead of trying to go all the way back to where it was it will move to the closest loc and then make sure it is at a safe distance from the mob(s).
  * Added MinBuffCheckTimer to the ini (See ini changes for more details)
  * Added LootReturnNearestLoc to the ini (See ini changes for more details)
  * Added Alerts (See ini for setup details)
    * You can now specify audio alerts for when you come accross a specific mob or if you die.  I can add more alerts if people want, just let me know what yall would like.
  * The mage will now attempt to gate in some situations to avoid death or being stuck (I've caught mine a few times running into a wall because of being stuck)  If you have the Gate aa it will use it, if not it will attempt to mem and use the spell.

## INI Changes ##
  * New MinBuffCheckTimer, this is only used in GroupMode so it is under GroupSettings.  It makes it so that it will only check buffs once every specified period of time.  This will prevent it from constantly cycling targets during downtime.  You can use any time in the form of s or m (example 30s for 30 seconds or 1m for 1 minute).
  * New LootReturnNearestLoc, this option if set to true will make the mage return to the nearest loc after looting a corpse instead of going back to the loc it was at when the mob died.  This is usefull in areas where you may not be able to return to the loc you were at (example the edge of a wall)
  * Changed buffs and combat spells to be able to use alt or items.  To make this change all xxxBuffItemx ini entries have been changed to xxxBuffSlotx, and all SpellGemx have been changed to SpellSlotx.  Valid entries for these are gem1 to gem10, item, or alt.
gemx only tells it where to mem the spell if it is not already memmed.
item tells it that the spell is being cast from an itm
alt tells it that the spell is being cast from an alt ability
So lets say for example you want to use the new SoD Group Invis aa when you are buffing.  Your entries would look like this:
```
SelfBuffName1=Perfected Group Invisibility
SelfBuffText1=Perfected Group Invisibility
SelfBuffSlot1=alt
```
I'd recommend if you did use something like invis, it needs to be your last buff so that you don't cast another buff and break your invis (buffs are cast in the order they are appear in the ini).
  * Removed all limits from the ini
No longer do you have a limit to the number of buffs or spells that you can have in the ini.  Each section has a Value setting that should be set to the number of items in that section.  So if you are using 5 spells the value in Combat should be set to 5.
  * Added Alerts section to the ini.
You can now have audio alerts if you encounter a specific mob, or if you die.  The settings are as follows:

  * [Alerts](Alerts.md)
  * AlertDeathAudioFile=c:\music.mp3  _This is the audio file it will play if it dies.  You can set it to null to not play anything if you die._
  * Value=1 _The number of mob audio alerts_
  * AlertMobName1=rat _The name of the mob you want to set the alert off (it can be a partial name)_
  * AlertAudioFile1=c:\music.mp3 _The audio file it will play if it targets this mob_

For alerts it will keep track of up to 100 npc ids that it is currently playing alerts for.  It will erase the id if that spawn is no longer in the zone.  I can't imagine anyone being engaged in more than 100 mobs at a time all having an alert, but if you do it will not play alerts past 100 alerts at the same time.


---


## Future Additions ##
  * Ability to summon and equip pets
  * Ability to accept rezzes

**Please I welcome comments, suggetions, and change requests!**