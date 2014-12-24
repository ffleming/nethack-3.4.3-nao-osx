NetHack 3.4.3, NAO version, for OSX
===

This repository contains a fork of the [nethack.alt.org](http://nethack.alt.org) repository.  The NAO version of nethack contains the following patches (from [NAO's version information](http://alt.org/nethack/naonh.php))

Automated installation
---
The purpose of this repository is to allow a more playable (i.e. heavily patched, but not in a play-altering way) version of Nethack to be easily installed via the Homebrew package manager.  If my (forthcoming) PR is accepted, installation will be as simple as
```
% brew install nethack
```
Until then, however...

Manual installation
---
1. Clone the repo
    ```
    % git clone git@github.com:ffleming/nethack-3.4.3-nao-osx.git
    ```
2. Enter the repo
   ```
   % cd nethack-3.4.3-nao-osx
   ```
3. Setup (no autoconf here!)
   ```
   % sh sys/unux/setup.sh l
   ```
4. Build
   ```
   % make
   ```
5. Install
   ```
   % sudo make install
   ```

New changes
---
* Necessary alterations for compiling on OSX
* Install to `/opt/nethack`
* Define SHELL to allow use of `!` to drop to a shell
* A [patch](https://raw.githubusercontent.com/ffleming/nethack-3.4.3-nao-osx/master/nethack-3.4.3-nao-osx.patch) against vanilla nethack 3.4.3 for use by [Homebrew](http://brew.sh/) via `brew install nethack`

The patch
---
Created with `diff --exclude=.git* --exclude=*.diff --exclude=*.patch -rupN "$VANILLA_DIR/" "$PATCHED_DIR/" > "$PATCH_FILENAME"`

Changes implemented by NAO
---
* Fixed several bugs:
     * C343-19 Dipping acid in a fountain may not destroy the acid. (Patric Mueller)
     * C343-52 Worn or wielded objects destroyed by dipping into lit potions of oil are not handled properly (Patric Mueller)
     * C343-74 Entering a long running, uninterruptible command after stoning starts will kill you. (Patric Mueller)
     * C343-98 Reset stored ID of quest leader when undead-turned, allowing #chat to work properly. (Steve Melenchuk)
     * C343-100 Game may crash if thrown potion hits bars before a monster. (Patric Mueller)
     * C343-171 Silver weapon damage message is sometimes missing when hero is polymorphed (Patric Mueller)
     * C343-172 Crash could occur when monster uses potion or food to cure stoning or confusion. (Ray Chason)
     * C343-179 If a monster is killed or tamed while over water (or by a drawbridge) while carrying a potion of acid, the game may panic. (Patric Mueller)
     * C343-189 Temple donations and protection lost to gremlin attack interact incorrectly. (Patric Mueller)
     * C343-198 Playing in a 20 or 21 line window can cause the game to crash.
     * C343-218 Applying a wielded cream pie can crash the game.
     * C343-231 Time is distorted while sinking into lava. (Patric Mueller)
     * C343-235 Casting spell of protection gives incorrect message if hero is swallowed or in rock. (Patric Mueller)
     * C343-268 Used up potion of acid may end up in bones file. (Patric Mueller)
     * C343-275 If a lit, wielded, candle or potion of oil burns out, the game may crash.
     * C343-276 If a figurine auto-transforms while wielded or worn, the game may crash.
     * C343-317 Bones data can contain odd characters from player's dogname, catname, or fruit options; this can cause odd terminal-dependent behavior.
     * C343-320 Reading a scroll of mail breaks illiterate conduct.
     * C343-324 Cutting a long worm in two will crash the game if the cut takes the worm to 1 HP or if long worms had become extinct. (Patric Mueller)
     * C343-349 An identify scroll is wasted if space is typed and steps off the end of the inventory list. (Steve Melenchuk)
     * C343-439 Running NetHack in a terminal window with more than 255 rows or columns produces display errors. (Patric Mueller)
     * SC343-11 It's possible to easily find the identity of a high priest on the Astral plane.
     * SC343-12 Hero using telepathy can abuse Call on the Astral Plane. 
     * SC343-20 Hangup save while picking up gold in a shop may duplicate the gold. (Patric Mueller)
* Added the [Curses windowport](http://nethackwiki.com/wiki/Curses_interface), with a fix for monster detection not waiting for --more--.
* Added boolean option [quiver_fired](http://bilious.alt.org/?287) (Patch by Jukka Lahtinen)
* [Sortloot](http://bilious.alt.org/?42) (by Jukka Lahtinen), with more sorting types from UnNetHack (by Patric Mueller)
* Pressing cmd key at direction prompt selects previously selected direction. (Patric Mueller, unnethack r844)
* The impossible-warning tells to save, not quit.
* Livelog reporting (for IRC, etc)
* Whereis-file user tracking, from SporkHack, with minor changes.
* Random player statues takes names from top1000, not top10
* Several new T-shirt messages, random epitaphs and engravings, hallucinatory monsters
* Changed 'C' to present a menu, and added old_C_behaviour boolean option to restore vanilla 3.4.3 monster christening behaviour
* [Dungeon colors](http://bilious.alt.org/?17) -patch (Pasi Kallinen)
* Changed 'X' to toggle twoweapon instead of trying to enter explore mode
* [Extinct and Showborn](http://bilious.alt.org/?43) -patch (Jukka Lahtinen)
* [Paranoid Quit](http://bilious.alt.org/?44) -patch
* [Window edge](http://bilious.alt.org/?14) -patch (Pasi Kallinen)
* [Dumplog](http://bilious.alt.org/?40) -patch (Jukka Lahtinen), with some minor changes
* [Menucolors](http://bilious.alt.org/?11) -patch (Pasi Kallinen)
* <s>[HitPoint Monitor](http://bilious.alt.org/?45) -patch (Ralph Churchill)</s> (removed)
* Simple Mail -patch, from [dgamelaunch](http://nethackwiki.com/wiki/Dgamelaunch)
* [Extended Logfile](http://bilious.alt.org/?289) -patch (Aardvark Joe), with some small changes
* A boolean option 'bones' to disable bone-file loading.
* [Messagetype-option](http://bilious.alt.org/?397) -patch (Pasi Kallinen)
* A patch to allow server admin to notify players.
* A patch to allow NetHack output special escape codes (vt_tiledata -boolean option)
* [fcntl locking](http://bilious.alt.org/?412) -patch
* [use_darkgray](http://bilious.alt.org/?205) -patch (Michael Deutschmann)
* [Show BUC](http://bilious.alt.org/?198) -patch (Pasi Kallinen)
* [Show Sym](http://bilious.alt.org/?15) -patch (Pasi Kallinen)
* [While Helpless](http://bilious.alt.org/?12) -patch (Pasi Kallinen)
* A patch to make RNG prediction harder
* Make NetHack assume the clearscreen escape code is always available, instead of complaining.
* Fix 100% CPU usage when terminal closed at a --more--- prompt. (tty windowport)
* Make cursor keys not escape out of a text entry prompt (tty windowport)
* Added [Pickup thrown](http://bilious.alt.org/?98) -patch (Roderick Schertler)
* Added a modified version of [key rebinding](http://bilious.alt.org/?148) -patch (Jason Dorje Short)
* Added a generic item use menu (from AceHack, via UnNetHack)
* Added [monster targeting](http://bilious.alt.org/?415) -patch (Pasi Kallinen)
* Force a screen redraw every 2k turns after the previous screen redraw.
* Fixed farlooking at food items in curses windowport.
* Prevent the Book of the Dead from being destroyed when falling into (or walking over) lava without fire resistance. (Steve Melenchuk)
* Added `botl_updates` option to prevent status line updates, and extended command `#updatestatus` to force an update.
* Added `hp_notify` option to turn on HP change notifications in the message lines, and `hp_notify_fmt` to configure the notification format.
* Changed TTY msghistory maximum to 400.
* Added [Statuscolors](http://bilious.alt.org/?142) -patch. (From UnNetHack)
* Added hitpointbar (from UnNetHack)
* Added boolean option msgtype_regex, if true, MSGTYPE-lines use regular expressions instead of globbing.
* Added boolean option apexception_regex, if true, AUTOPICKUP_EXCEPTION-lines use regular expressions insteaed of globbing.
* Show shop prices when walking over the items in the shop. Turn off with show_shop_prices option. (from UnNetHack)
* Added item_use_menu boolean option, to turn off the generic item use menu used via inventory.
* Added msg_wall_hits boolean option. If true, mentions in the message area whenever you walk against a wall. Useful for blind players.
* Added item glyphs (colored symbols) to tty menus. (from UnNetHack) Boolean option menu_glyphs to turn them on and off.
* Fixed option parsing causing buffer overflow. (Found by Matthew Daley)
* Write extra info file for dgamelaunch use.
* Prevent [artifact naming](http://nethackwiki.com/wiki/Artifact_naming).
* Fix several crashes in case makemon() returns null. (From UnNetHack r1067)
* Record HUP exploits into a file.
* Fix some crashes related to displaying ball/chain and beam glyphs.
* Fix a crash with hitpointbar. (From UnNetHack)
* New boolean option "hilite_hidden_stairs", will try to show item with red background, if stairs are underneath it.
* New boolean option "hilite_obj_piles", will try to show item piles with blue background.
* Bugfix: prevent dangling pointer when applying a container that might have been destroyed (Patric Mueller)
* Added "View discoveries" -option to the #call menu
* Added MONSTERCOLOR config option (From UnNetHack)
* Made STATUSCOLOR support exact numbers, eg. `STATUSCOLOR=hp.1:red&inverse,hp<8:red,hp>50:grey`
* Fix TTY crashing when a location has more than 32k item stacks
* Fix impossible() giving out faulty values (Pat Rankin)
* Curses: Fix 100% CPU usage when terminal was lost at DYWYPI prompt
* Curses: Fix selecting parts of multiple stacks (Alexander Gabriel)
* Prevent perm -file lock from staying around when terminal is closed at "Destroy old game" -prompt.
* Fix a crash when restoring a game when riding and detecting monsters. (Patric Mueller)
* Fix segfault when teleporting onto a sink while equipping levitation boots. (found by Alex Smith)
* Fix a crash when picking up an unpaid object from a location shared between two shops. (Patric Mueller)
* Fix scroll of charging not working when used via item_use_menu.
* Experimental support for UTF8 graphics. (Patric Mueller)
* Implement menu_search for windowtype:tty
* Curses: Actually show the "Destroy old game" -prompt
* Fix stat abuse of gauntlets of dexterity and helm of brilliance (by Alex Smith)
* Multiple possible bones files per level (via UnNetHack)
</ul>
