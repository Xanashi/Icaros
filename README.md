Description
===========================

Icaros Shell Extensions - A Shell Extensions Framework By Xanashi


Icaros is a collection of lightweight, high quality, Windows Shell Extensions.

Icaros can provide Windows Explorer thumbnails, for essentially any video media format supported by FFmpeg, 
this includes popular filetypes such as: Mkv, Flv, Avi, Mp4, Mov, Rmvb, M2ts, Ogm etc.

Besides the FFmpeg supported filetypes, Icaros also contains custom parsers, 
which can produce Cover Art thumbnails for Mkv, Flac, Ape, Mpc and several other filetypes.

Icaros also provides Windows Explorer properties for the following popular filetypes:
Mkv, Mk3d, Webm, Ogm, Ogv, Ogg, Flv, Avi, Xvid, Rm, Rmvb, Flac, Opus, Spx, Ape, Mp3, Mpc, Mka, Tak, Tta, Ofr, Ofs, Wav, Wv

Properties refer to the info shown for each file in Explorer, such as length, width, height, title, channels and so on.

Icaros works on Vista, Windows 7, Windows 8/8.1 and Windows 10.

Icaros 3.0.3 and previous versions works partially on Windows XP (SP2+) (Thumbnails only).




Requirements
===========================

The Icaros shell extensions have no dependencies.
If manually registered, they should work right away on any of the supported systems.
Check the 'Manual Registration' section below for further information. 


There are two exceptions. On Windows XP the Icaros Property Handler is not supported, due to the 
way XP handles file properties, and on Windows XP SP2, one additional library is required for the 
Icaros Thumbnail Provider to work.
The library can be downloaded here:

32-bit: https://download.cnet.com/Microsoft-Windows-Imaging-Component-32-bit/3000-12511_4-75578540.html

64-bit: https://download.cnet.com/Microsoft-Windows-Imaging-Component-64-bit/3000-2192_4-75578538.html

NOTE: enu is English


IcarosConfig (the GUI) requires .NET Framework 4.
The Icaros installer should automatically install .NET 4, but in case .NET 4 is not installed 
on your system after installation, you can download and install it with the following URL:

https://www.microsoft.com/en-us/download/details.aspx?id=17851




Installation/Activation
===========================

By default Icaros only registers a number of common 'thumbnail' filetypes during activation,
but in principle it is possible to register any filetype supported by FFmpeg, 
along with a number of other filetypes, which is supported natively by Icaros.

If you're in doubt whether a filetype is supported or not, please try dropping a file of that filetype,
onto the 'THUMBNAILING' page in IcarosConfig. Icaros will then check the filetype and add it, if it's supported, 
or show a dialog if it's not supported.

If a filetype is already registered to another shell extension, then Icaros will remember the previous shell extension, 
and during deactivation (or removal of the filetype from Icaros), reinstate the old shell extension for the specified filetype.

Activating Icaros is simple:


 1. Open IcarosConfig.exe, with administrative privileges.

 2. The second column from the left is the 'Activation Panel'. In this panel you can see each Icaros component,
    as well as their activation state (e.g. THUMBNAILING - DEACTIVATED).
    To activate a feature, just click on the name of it to change its state. 
    
    Thumbnailing and properties can either be activated or deactivated.
    Cache can be Disabled, Enabled (Static) or Enabled (Dynamic) (see Icaros Cache section below for more info).

 To Deactivate/Unregister Icaros, click the name again to change the state once more.




Shell Extension Options
===========================

Each component in Icaros has several options, that allows you to tweak the overall experience of Icaros.
To the left of each component name and state, an icon for that component is located. 
Click these icons to access each specific component's page of options.

Below is a description of some of the most important options available (excluding the cache options, which is described further below).

Remember all of the below options can be utilized even while Icaros is Active.
IcarosConfig will automatically handle any changes on-the-fly.



THUMBNAILING OPTIONS

 - There are now four different ways to add new thumbnail filetypes, as opposed to the previous IcarosConfig which only had one.

   1. The first way is through Presets. 
      As the name implies, Presets are pre-configured lists of thumbnail filetypes.
      This feature was added, as a "set-once" kind of option for new users, to apply a large amount of well known (working) filetypes, with two simple clicks.
      Just open IcarosConfig and select a preset that match your needs, and that's it.

      If you currently have filetypes registered which are not included in a selected preset, IcarosConfig will prompt whether to discard or keep those filetypes.


   2. The second way to add filetypes is via the "Add New Filetypes" button to the right of the filetypes box.
      This will bring up an Open File dialog, from where you can select any number of different files, and simply click 'Open' to add their filetypes.

      However, before adding the filetypes, IcarosConfig will perform a "thumbnail check" on each file selected, and test if a thumbnail can be 
      created from them. If one or more files fails this test, the user will be notified (after all files have been checked), and can ultimately decide
      whether to discard or apply the failed filetypes.


   3. The third way is through Drag 'n Drop. 
      This is another quite easy way to add new filetypes. If you Drag n Drop files and/or folders unto the thumbnail page, IcarosConfig will automatically
      perform the actions from [2.] on each file dropped.
      Dropping a folder is basically the same as dropping all the files of that folder. All subdirectories will be ignored.


   4. The final way is the same as in the previous IcarosConfig.
      Click the Thumbnail Filetypes textbox to make the filetypes string editable, then modify the string by adding or removing filetypes
      using the following syntax: avi;flv;mov;ogv;flac
      Notice that the list is semi-colon separated and filetypes can optionally be preceded by a period '.'.

      This is currently also the best way to remove singular filetypes from the list too.


 - It is possible to set the thumbnail offset in percent or as a timestamp in milliseconds.
   This will determine, at what position in the stream/file, the frame (thumbnail) will be grabbed.
   If the timestamp is preferred, Icaros will first try to grab the frame from the specified timestamp,
   and if it fails to do so, it will then fall back to using the percentage offset.


 - With the 'black/white frame detection' option enabled, Icaros will perform a quick and simple
   scan of the grabbed frame. If the frame is either too dark or too light, Icaros will skip 
   forward and try to find a better suited frame.
   
   The threshold determines the aggresiveness of the scan (0-30%). 
   The default value is 8%. The higher the value is set, the more sensitive the scanner will be, and more frames will be detected as 'unsuited'.
   This can have the negative effect of making the overall thumbnailing slightly slower.
   It is recommended to leave this option at its default value.


 - Icaros has a quick shortcut, that allows you to disable/enable the small icon overlay located at the bottom right of each thumbnail.


 - When Cover Art is enabled, Icaros will look for embedded cover art in files, that support cover art, while generating thumbnails.
   If a cover is found, it will be used as thumbnail, otherwise Icaros will automatically fall back to normal thumbnailing.

   Some MKV files contain multiple covers. With such files Icaros will default to using the first normal/vertical cover.
   Setting the 'Prefer Landscape Covers' option will make Icaros prioritize landscape/horizontal covers instead.

   Note: This should not affect the thumbnailing speed in any noticable way.



PROPERTY OPTIONS

 - You can enable/disable Explorer Properties for specific filetypes via the checkboxes located on the PROPERTIES page. 
   If all checkboxes are disabled, the property handler will not be registered, during activation.




Icaros Cache
===========================

The Icaros Cache was implemented as a counteract to the issue where Windows deletes its own thumbnail cache.

If the Icaros Cache is enabled, Icaros will be able to store a copy of any thumbnail in an internal cache, and if for some reason
Explorer deletes its own thumbnail cache, Icaros will be able to regenerate all the thumbnails again at almost instant speed.

If the Cache is disabled, it wont have any impact on the thumbnail provider at all. The thumbnail provider will just work like 
it did in previous versions of Icaros. 

The Cache was designed to deliver thumbnails to Explorer at the highest possible speed, however Explorer still needs to process 
each thumbnail (i.e. validate, crop, apply adornments, and add it to the Windows cache), so you may still experience a small 
rendering delay even when the cache is used.


The Icaros Cache can be utilized and managed in a number of ways. Below is a quick walkthrough.


 1. The Icaros Cache has 3 activation states:

    - Disabled:           Cache disabled
    - Enabled (Static):   Icaros Thumbnail Provider will use the cache, but without adding any new entries to it. IcarosConfig can still modify the cache (see below).
    - Enabled (Dynamic):  Icaros Thumbnail Provider will use the cache, and add new entries to it dynamically, as it thumbnails files that are not yet cached.


 2. On the CACHE page of IcarosConfig, you can find several options for the internal cache:

    - Max Cache Size:      Allows you to set a maximum limit for how large the Icaros Cache can get in MB. 0 is unlimited.
    - Min Free Space:      Allows you to limit the cache from growing further, if the hdd the cache is located on only has limited space left. 
    - Cache Location:      Gives you the option to change the default cache location.
    - Excluded Filetypes:  A list of filetypes which won't be added to the internal cache. A number of image formats is added by default,
                           as they rarely gain any benefits from being added to the internal cache.


 3. On the CACHE page of IcarosConfig, another feature, known as the Cache Indexer, is available.
    The Cache Indexer allows the user to fill up/clean up the Icaros Cache directly from IcarosConfig.

    The Cache Indexer can be used even before Icaros has been activated, so it can be used to pre-thumbnail
    all your files, right after installing Icaros.

    1. To start using the Cache Indexer, add one or more folders to the LOCATIONS tab on the CACHE page.
       These folders should contain the files which thumbnails you want added to the internal cache.

       Be sure to set the same 'View Size' for each folder as you use in Windows Explorer.
       If 'Recursive' is checked, the Cache Indexer will also index all subdirectories found in that folder.

       If you want all subdirectories to be indexed, except one or two, you can use the 'Excluded Locations' list
       to add these directories.

       It is possible to drag 'n drop folders to the LOCATIONS tab directly from Explorer to add them to either list.

    2. Go back to the SETTINGS tab and click the 'BUild Cache' button, to start filling the cache with entries from
       the included locations.

    3. Once the indexer has completed, make sure Icaros Thumbnail Provider is ACTIVATED and the Icaros Cache is ENABLED.
       Browse to any of the included locations, which has yet to be thumbnailed by Icaros, to see the internal Cache in action.

    4. To clean up the existing cache (removing unused entries, and adding new entries from recently created files),
       click the 'Rebuild Cache' button.

       Be sure to use this button as well, if you're adding or removing folders on the LOCATIONS page.
 
       Be careful rebuilding your cache when using the DYNAMIC mode, as all dynamically entries will be removed 
       when the cache is cleaned up.       

    5. Finally it is possible to delete the internal cache by clicking the 'Clear Cache' button.
      

To avoid having entries disappearing unintentionally from the internal cahe, Icaros does not have any automatic clean up routines of the internal cache. 




Manual Registration
===========================

To register/activate Icaros manually, follow these steps:


 1. Open a command prompt, with administrative privileges

 2. (Optional) All Icaros Thumbnail Provider and Icaros Property Handler options can be managed via the following registry keys:
    (Icaros will automatically use the default values, if any of the following values are not set) 

     Windows Registry Editor Version 5.00

     [HKEY_LOCAL_MACHINE\Software\Icaros]
     "Thumbnail Extensions"=".mkv;.flv;.mov;.ogv"  <-- Filetypes that will be registered by the thumbnail provider
     "Excluded Properties"=".ogm;.ogv;.ogg"	   <-- (Optional) Excluded property filetypes (default: none are excluded)
     "Prop Local"="ru"	                           <-- (Optional) If a localization file is present, this value determines what language the
                                                                  Icaros Explorer properties will show up in after registration.

     [HKEY_CURRENT_USER\Software\Icaros] 
     "Cache"=dword:00000001 		           <-- (Optional) Enable Icaros Cache (0: disabled 1: enabled (static) 2: enabled (dynamic))
     "Offset"=dword:00000023 		           <-- (Optional) Set thumbnail offset in percent in hex
     "TimeOffset"=hex(b):10,27,00,00,00,00,00,00   <-- (Optional) Set thumbnail offset in milliseconds in little-endian hex
     "UseCoverArt"=dword:00000001		   <-- (Optional) Enable Cover Art in mkv (0: disabled 1: use normal cover 2: use landscape cover)
     "FrameThresh"=dword:00000008                  <-- (Optional) If this value exists, Icaros will try to detect black and white thumbnails and replace them
                                                                  with a better frame from the file. The value itself determines how aggresive the scan will be.
                                                                  The value can be from 0 to 30. 30 being the most aggresive, changing more frames.
                                                                  It is recommended to leave this value at 8.

     [HKEY_CURRENT_USER\Software\Icaros\Cache] 
     "ExclExts"="jpg;png;gif"                      <-- (Optional) Filetypes that will be ignored by the Icaros Cache
     "MaxCacheSize"=dword:000001f4		   <-- (Optional) Set the maximum cache size in hex (0 is unlimited)
     "MinFreeSpace"=dword:00000800		   <-- (Optional) Set the minimum free space in hex (default is 1024MB)



 3. Run the following command:        RegSvr32.exe "Path\To\IcarosThumbnailProvider.dll"
                           or:        RegSvr32.exe "Path\To\IcarosPropertyHandler.dll"

 4. To unregister, run this command:  RegSvr32.exe /u "Path\To\IcarosThumbnailProvider.dll"
                                 or:  RegSvr32.exe /u "Path\To\IcarosPropertyHandler.dll"


Note: If you're on a 64-bit system, make sure you register the dlls located in the 64-bit directory.
      If you need to enable Icaros in 32-bit dialogs on 64-bit systems, you must also register the dlls
      located in the 32-bit directory.




Additional GUI Features
===========================

If you click the gear icon in the upper right corner of IcarosConfig, you'll find the 'ui settings' page.
On this page, a wide range of options allows you to customize the look, interactions and language of IcarosConfig.

Changing the language here also gives you the option to change the language of the property labels in Windows Explorer.




Donations
===========================

If you like Icaros and wish to support the free development of the project,
please consider making a donation to the developer. 

Donation link: 
https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=A4SV4449UB4UQ&lc=GB&item_name=Project%20Icaros&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted




Translations
===========================

If Icaros isn't currently translated in your language, and you wish to help out with the translation,
please check out this simple guide on how to translate Icaros:

http://shark007.net/forum/Thread-How-to-Translate-Icaros?pid=37920#pid37920

Be sure to contact me at Xanashi[at]gmail[dot]com, if you have any questions or have a translation
file completed, and I'll be sure to include it in the next release of Icaros.




FFmpeg Info
===========================

Icaros is using the free software project FFmpeg, to extract frames from various media files.  
FFmpeg is licensed under the LGPLv2.1, which you can find in the Licenses directory of Icaros,
or read online at: http://www.gnu.org/licenses/lgpl-2.1.txt

Icaros is using nevcairiel's fork of FFmpeg, which contains various fixes and improvements.
The source code for this fork, can be browsed online here: http://git.1f0.de/gitweb?p=ffmpeg.git;a=summary

Great thanks to both nevcairiel (LAV Filters, http://1f0.de/) and the FFmpeg Team (http://ffmpeg.org/)
for all the hard work they've put into FFmpeg.



