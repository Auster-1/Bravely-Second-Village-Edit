# Bravely Second Village Edit
A simple bash script for editing your Village population count in Bravely Second: End Layer.

This script recreates the function of ukee's fork from GBA Temp, which is no longer available.

The purpose of this script is to restore functionality to the Village feature in <a href="https://en.wikipedia.org/wiki/Bravely_Second">Bravely Second</a>. The Village is a reward system that, much like its Bravely Default counterpart, progressively unlocks items and customization options for the player as residents of the village complete the repair of various buildings over time.  The player only begins with 1 resident with the expectation that they will collect more via the Nintendo 3DS's StreetPass feature or by using the Update Data option at Save Points.  Both options require you to either be in regular proximity to another 3DS with physical hardware or to connect to Nintendo's 2012 servers, neither of which are achievable via modern emulation, and with actual hardwares, Update Data is no longer an option and StreetPass is unlikely to be feasible.

The majority of building repairs take a prohibitively long time to complete with just 1 resident, with some jobs requiring the game be open for as long as *99 hours*, however each additional resident assigned to a job significantly reduces the time it takes to complete, so this script serves to manually edit the number of residents in Norende Village.

***Warning!:*** *Editing saves always carry a risk.  BACKUP YOUR SAVE FILES before making any edits.*

Tested on an emulator-generated save, but maybe it works on 3DS saves too if the saves are dumped through JKSM.

## Save Editing
Download the script, put it in the same folder as the `BD2COLONY#.sav` file to be edited (`#` being the number of the file) and run the following Terminal command from the same directory:
```
bash bravelyedit.sh
```
In the Terminal you will be prompted to enter the save file you wish to edit (1, 2, or 3) and then enter your desired number of residents.  The script currently only accepts integers from 1 to 255.

The script will `exit` if
- you specify an invalid save file
- the specified save file doesn't exist
- you request a population count lower than 1
- you request a population count greater than 255

The script will inform you of your save file's population count before and after making edits.

## How does it work?
Your Village save data is contained in one of three hidden files called BD2COLONY#.sav.  The Village population count is stored in two hexadecimal bytes located at 0x4 & 0x5.  Bravely Second Village Edit reads your chosen save slot as a filepath then takes a decimal integer from you and converts it to hexadecimal before writing it to the file.

## Important Notes
Some useful information to bear in mind regarding Village save data editing:
- Village save data is created as soon as you start a new save file.
- Village becomes available in-game after Magnolia joins the party.

***Warning!:*** *The effects of decreasing an existing population count while you have residents assigned to jobs is currently UNTESTED.*

## Saves location
You may already know that the developers of Citra discontinued the project after legal action from Nintendo.  Consequently, the `flatpak` version, which this script presumed your use of, no longer launches.  As of 1.0.1, this script presumes you're using the `appimage` version of Citra and locates your saves accordingly.  If you had saves for another version of Citra that you'd like to copy over, saves for all 3 Linux releases can be found in these folders:

**Appimage:** `/.local/share/citra-emu/sdmc/Nintendo 3DS/00000000000000000000000000000000/00000000000000000000000000000000/title/00040000/000fc500/data/00000001`\
**Flatpak:** `/.var/app/org.citra_emu.citra/data/citra-emu/sdmc/Nintendo 3DS/00000000000000000000000000000000/00000000000000000000000000000000/title/00040000/000fc500/data/00000001`\
**Snap:** `/snap/citra-emu/common/.local/share/citra-emu/sdmc/Nintendo 3DS/000000000000000000000000000000000/000000000000000000000000000000000/title/00040000/000fc500/data/00000001`
**Retroarch:** `.config/retroarch/saves/Citra/Citra/sdmc/Nintendo 3DS/00000000000000000000000000000000/00000000000000000000000000000000/title/00040000/0017ba00/data/00000001/`
**JKSV save dump:** `/JKSV/Saves/BRAVELY SECOND/[user-named folder]`
