# Changelog

## 2.1.0
- Add support for point_hud_icon_(allies|axis|neutral) which define custom
  objective icons (icons that show the state of Day of Defeat control
  points on the HUD).

## 2.0.3

- New: Added -n option to preserve WAD files in .res file, even if unused.

## 2.0.2

- Bugfix: Fixed flawed logic that caused RESGen not to parse skynames and
  in some cases of non-standard BSP styles, the wad files. Thanks go to
  jtp10181 for finding this bug and suggesting a fix.

## 2.0.1

- Bugfix: Fixed minor bug in VString class that could occur if an empty
  string was concatenated with an existing. No know instances of this have
  occured because RESGen uses several sanity checks before doing string
  operations.
- Fix: RESGen only supported BSP files generated on Windows or Unix/Linux
  because of the way line endings are handeled. Support for BSP files
  generated on a Mac/Apple (or using Apple style newlines) has been added.
- Note: Decided to release this version as 'final' version 2. Note that
  this doesn't exclude any future bugfixes. It's just to indicate the
  current maturity of RESGen 2.

## 2.0 RC2

- Bugfix: Fixed bug in exclude file parsing. When the parser encountered a
  comment it would consider every following line a comment as well because
  it failed to clear the line buffer.
- Bugfix: Fixed bug with loading exclude files. Forgot to convert
  backslashes to slashes, which means that any exclude located in a folder
  would never be matched if the exclude file used Windows format.

## 2.0 RC1

- Fix: Made some improvements to memory cleanup at program termination.
  While this probably doesn't make any difference to program preformance,
  it does score pretty high on the 'proper coding' meter.
- Merge: The changes made by Zero3Cool have been merged with BETA 3 to
  supply you with the very best of RESGen in 1 great package!
  Zero3Cool's changes are:
  - Added -g flag (Displays content of generated .res files. By default
    RESGen will now NOT show this by default (causes slower
    performance)).
  - Added -b [rfafile] flag (Exclude resources from [rfafile] from being
    added to generated .res files).
  - Changed -i flag to display found maps while searching folders.
  - Removed some verbality to speed things up.
- Fix: To keep in 'spirit' with Zero3Cool's changes, the -s and -j
  switches have been altered to display extra output instead of preventing
  output to show up.
- Fix: Removed some more verbality for -v mode. Output is now bare
  minimum.
- Fix: Rewrote Zero3Cool's parsing code for excluding resources to be more
  reliable.
- Fix: Rewrote list lookups (used with resource verification and resource
  exclusion). Due to the new lookup system parsing speed should increase a
  lot over previous versions if these options are used.
- Fix: Fixed some VString bugs (RTrim was broken) and some other minor
  changes. Added extra compare function.
- Upgrade: Upgraded LinkedList with some improvements made earlier, but
  which were not yet integrated with this version. Added sorting and find
  functions to sort the lists. The find function can rapidly find a node
  in the list, provided it's sorted. To extend the usefulnes of the
  LinkedList class and to further optimize sorting an InsertAt and
  InsertSorted function has been added.
- Fix: Fixed some small errors in LinkedList and VString classes and added
  some functionality. If you are using these classes in another project it
  is recommended you upgrade them with these new versions.
- New: Added case correction for res file entries with -m switch. For it
  to operate resource verification (-e) should be used. It uses the
  resource list built with resource verification to correct case.
  -m overrides -l.
- Fix: In overwrite mode (-o) res files will be deleted if there are no
  resources found. This prevents old res files from staying behind with
  wrong entries. This is especially the case when using options like -b
  or -e.
- Fix: Changed -l option to default NOT to convert entries to lowercase.
  You must now specify -l to have your entries converted to lowercase.
- New: Added WAD file parsing. RESGen will now check if a WAD file
  actually contains textures used by the map. It also reports any missing
  textures. Use the -u switch to activate the checking.
- New: Added MLD file parsing. RESGen will now check if a MDL file
  requires a seperate texture file. If it does, this texture file is added
  to the res file. Use the -u switch to activate the checking.
- New: RESGen reports res files that have missing resource because they
  were not found (only applies to -u and -e options). Use -g to see which
  wad files resources are missing and which resources were excluded.

## 2.0 BETA 3

- Bugfix: Overviews were not properly added to the res file. RESGen
  only looked for a bmp file. To make matters worse, it added it as a tga
  file to the res file. This behaviour has been corrected. RESGen now
  looks for a tga and a bmp file (favouring the tga if both are present).
- Fix: Half-Life already transfers the map's txt file to the client,
  without looking at the res file. RESGen used to add this txt file to
  the res file too. Since this is not needed and can even create errors,
  RESGen now does not add the map's txt file to the res file.

## 2.0 BETA 2

- Bugfix: The parsing enigne crashed when the BSP entity data wasn't in
  Linux format. It now can work with data in Windows format too. If the
  BSP is in any other format, the parser will generate an error, instead
  of crashing.
- Bugfix: If there were no WAD files specified for a map, the parser gave
  an error message for the map and stopped parsing it. It now correctly
  handles this and can continue parsing the rest of the BSP.
- Fix: Entity data corruption errors now give a bit more information about
  what is wrong with the data.
- Bugfix: While running RESGen I discovered that the memory use increased
  with every parsed map. After running a memory leak detector and
  reviewing the code, I discovered that I forgot to close the BSP files
  after reading them (*doh*). They are now properly closed and there is no
  more memory leaking. (That I know of anyways :)

## 2.0 BETA 1

- New: Initial release. Total rework of the parsing engine. Also much more
  object oriented.

## Changes between v1 and v2

From the outside RESGen 1 and 2 look similar. On the inside a lot of changes have been made. First of all, major parts have been rewritten, and other parts have had a major upgrade. The biggest change is that the RESGen core is fully C++ now, instead of a bit C++ in a C program. Because of this I have DROPPED the scripting return values. It's very easy to use the RESGen source in your own programs now.

The RESGen parser should be a bit faster now. It's speed mainly depends on the speed of your hard disk and your output window. That last limitation can be overcome by using the -v option (minimal output).

The last major change is the -e option. It enables you to have RESGen automatically verify if you server actually has the resources the map claims to need. This especially applies to missing wad files. See chapter 5 for more information on how to use the -e option.

Additionally, RESGen now tries to locate the maps information txt and overview pictures. Please note that RESGen can only find these if they are stored in the same folder layout as they would be on the server (mapname.txt, ../overviews/mapname.txt and ../overviews/mapname.bmp).
