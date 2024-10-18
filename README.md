# RESGen #
RESGen is a tool to create res (resource) files for Half-Life. If a Half-Life map has a corresponding res file, Half-Life is able to send all resources the resources the map uses to the clients, if they don't have them. This helps a great deal when running a server with custom maps, instead of the defaults. Most players do not have these custom maps and the resources that should go with them. The res file enables them to download the map via Half-Life and start playing right away.

The problem with res files, however, is that it can take hours to create one if the resources used by a map are not known. RESGen can shorten this time to mere seconds. It reads the maps BSP file and searches it for used resources. The results of this search are then used to create the res file.

## Usage ##
* -a [rfafile]
  * The contents of the rfa file will be added to the end of the res file. This is useful when adding custom resources, like the StatsMe sound pack. The .rfa file extension is optional.
* -b [rfafile]
  * Excludes generated resources listed in [rfafile] (Default exclude .rfa's included). Useful to avoid log spam and steam http download problems. It is recommended to use this feature for steam servers, but note that it causes a speed decrease generating the res files.
* -c
  * Displays the RESGen credits.
* -d [folder]
  * [folder] will be searched for bsp files. A trailing (back)slash is optional.
* -e [modpath]
  * Makes RESGen verify that all resources in the res file actually exist. Resources that can't be found will be excluded from the res file. RESGen expects modpath to point to a valid mod directory structure. If the modpath isn't the valve folder, RESGen will try to find the valve folder too, so a complete resource list can be established.
* -f [map]
  * A res file will be generated for [map]. The .bsp file extension is optional.
* -g
  * Displays content of generated .res files and reports all missing resources. Causes slower performance.
* -h
  * Displays the help screen.
* -i
  * Displays maps found while building the map list. Only useful with the -r and/or -d option.
* -j
  * Resources found while building the resource list will be displayed. Useful with -e option.
* -k
  * Windows only. RESGen will not wait for the user to press a key to exit.
* -l
  * Turns on converting all res file entries to lowercase. RESGen converts all res file entries to lowercase since this is the default for Half-Life files. It has to do this because a lot of resource files in maps don't have the proper case that matches the actual resources. Only use this option if you know what you are doing.
* -m
  * Matches the case of the res file entries to the actual case of the files on disk. This prevents any missing resources because of wrong case in filenames. Recommended on Linux. If this option is used, the -l option will have no effect. Only works if used with the -e option.
* -n
  * Do not ignore unused WAD files. Necessary if the client insists on receiving all WADs referenced by the BSP, even if unused. Only works if used with the -u option.
* -o
  * If a res file already exists it will be overwritten. Removes old res files if the new file doesn't contain any res entries and no file is specified with the -a option.
* -p
  * Prevents RESGen from using the contents of any pakfile for resource verification. Thus, any resource that is available, but in a pakfile is excluded from the res file. This option is only useful when the -e option is also used. Please note that if a map comes with it's own pakfile, using this option will generate a res file that is incomplete.
* -r [folder]
  * [folder] and it's subfolders will be searched for bsp files. A trailing (back)slash is optional.
* -s
  * RESGen will display it's status line. This might considerably slow down res file generation, especially on smaller maps.
* -t
  * Linux only. RESGen will ignore symbolic links when searching folders for .bsp files. Please note that this does NOT affect resource searching. Useful with -d or -r options.
* -u
  * Parses relevant resource files to make sure they are actually used (such as WAD files) or to check if they have dependencies (such as MDL files with seperate textures). Only works with -e option.
* -v
  * Makes RESGen only give minimal output. It's recommended you use this if you want to create res files as fast as possible. RESGen will still report any error.
* -w
  * Displays the warranty for RESGen.
* -x [map]
  * Exclude this map from res file generation. Only works on maps found with -d or -r options. The .bsp file extension is optional.

Example 1:

  `resgen -ok -r C:\sierra\half-life\tfc -e C:\sierra\half-life\tfc -a shadowlord.rfa`

This will make RESGen generate res files for all maps that are in the tfc folder. It will verify it's resources from the tfc folder and the valve folder (C:\sierra\half-life\valve). Any existing res file will be overwritten. The contents of shadowlord.rfa will be added to all res files. When RESGen is finished it will exit immediately, not waiting for a keypress.

Example 2:

  `resgen -o -d C:\Sierra\half-life\tfc\maps -a customsounds.rfa -b res_tfc.rfa`

This will make RESGen generate res files for all maps that are in the maps folder. Any existing res file will be overwritten. The contents of customsounds.rfa will be added to all res files. Resources from res_tfc.rfa (these include valve resource) will not be added to generated res files.

### Using resource verification ###
The -e option, can be quite powerful. It can be used several ways. Here I try to describe a few of the more common ways, although there are many more.

NOTE: There is a subtle difference between Win32 and the Linux when checking if a resource is available or not. On Win32 RESGen does not care about case when comparing the found files to the res entry. On Linux it does care about it and reject resources when the case doesn't match. In 99% of the cases this doesn't matter. However, because of this difference it it's recommended to run RESGen on the target platform whenever possible.


Method 1, the simple way:

This method is most commonly used by server admins that want to add res files to their servers. Run RESGen on the mod folder you want to make res files for. Point the -e option to this folder too. This will generate good res files, which contain all found resources. You should not use the -p option unless you are certain that you have no maps with their own pakfile.

Example: `resgen -r half-life\cstrike -e half-life\cstrike`


Method 2, the mapper way:

You run resgen on the map, and point the -e option to the folder with the resources (these can be the same). Please note that the resource folder must match the folder layout of a normal folder. Using -p is possible if you aren't using a pakfile for your map. Also, note that resgen will look for the map info txt and overviews relative to the map itself, not the folder specified with -e

Example: `resgen -f mymap.bsp -e mapping\resourcetank`

## Credits ##
This program was made by Jeroen "ShadowLord" Bogers with serveral improvements and additions by Zero3Cool.

Special thanks to:
* "HoundDawg" and UnitedAdmins for helping RESGen grow.
* "Zero3Cool" for improving RESGen and keeping it alive.
* TheZProject.org for hosting RESGen.
* "luvless" for having the great idea to create this app.
* Valve for creating Half-Life!
* Everyone who uses RESGen.

http://resgen.hltools.com

## License ##
Copyright (C) 2000-2005 Jeroen Bogers, Zero3Cool

Copyright (c) 2013-2014 [GitHub contributors] (https://github.com/kriswema/resgen/contributors)

RESGen is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

RESGen is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with RESGen; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

