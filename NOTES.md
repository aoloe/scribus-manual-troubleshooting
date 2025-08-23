# Troubleshooting

What can you do when Scribus does not behave correctly?

Warning: it's very likely that it's not a good idea to create this document. Probably, we will move the content to each specific manual in a "Troubleshooting" chapter.

## Scribus is slow

- set the preview level to "small" in the outline window.

## Suddenly, I am no longer able to select frames and change their shape

- Are you on the correct layer?
- Is the layer locked?

## Missing fonts

Jean says : In any case you will have to reset font prefences by deleting the checkfonts.xml and
scribus150.rc files stored in preference folder, usually
C:\Users\username\AppData\Roaming\Scribus.

### Missing DejaVu

In the recent past (January 2017), Debian testing and Ubuntu 16.04/16.10 were distributing a version of the Freetype library (2.6.3) that was affected by a bug that prevented Scribus from loading outlines of some glyphs with the DejaVu font (and others).

Freetype 2.6.5 contains a fix for this issue. The fix might already be in the 2.6.4 version.

But your version of Debian/Ubuntu might still have one of the affected versions. 

Debian testing now has 2.8.0, which does not contain bug affecting the way DejaVu is seen by Scribus.  
Scribus will not automatically recognize again DejaVu, you first have to manually force Scribus to re-create the font cache by

  - quitting Scribus,
  - removing (or, better renaming) the ~/.config/scribus/checkfonts150.xml file
  - starting scribus
  
Debian Stretch (stable in July 2017) still has 2.6.3 and i'm not sure if it will ever get 2.6.5+ (the ones without the bug)  
The relevant bug in Debian was https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=837800 ... closed.

OpenSuse 42.3 and Ubuntu 17.04 also ship a Freetype package affected by this
issue. In both cases it is Freetype 2.6.3.

According to DistroWatch, OpenSuse Tumbleweed already ships FreeType 2.8.0 which is not
affected by this issue. Ubuntu 17.10 will have a FreeType upgrade as well and will also
come with FreeType 2.8.0 (or maybe 2.8.1, who knows?).

## Missing images

Scribus mostly uses absolute links to the images.

If you move the Scribus document with the images to a new folder or a new disk, it's likely that the images will not be rendered anymore (all the image frames will have a big red cross).

While the correct way to move a Scribus document is by using "File > Collect for output", Scribus allows you to relink all the images by using "Extras > Manage images":

- Start the "Extras > Manage images" tool.
- Click on one of the missing images.
- Click on the "Search" button and set "Start at" as the folder where images now are (or one of its parents).
- When the tool has found the image (by its name), select it, check "Apply to all matching images" and push the "Select button".

## I get the wrong colors from the printer

il y a souvent -- confusion entre des jolies images et des images correctes.

le fait que tes images soient jolies sur ton écran, n'a que peu à voir avec la qualité des images imprimées... sauf si tu as installé et activé les bons profils et calibré ton écran!


si tu as de bonnes photos (livrées par un photographe qui sait ce qu'il fait!), tu ne les a pas éditées sur ton ordinateur, tu n'utilise pas de profil colorimétrique et tu inclues les images telles quelles dans le pdf, dans ce cas elles devraient sortir correctes à l'impression.

mais c'est beaucoup de si... et si une seule de ces conditions n'est réalisée, ben, il n'y a pas grand chose qui soit encore assuré...  
même si avec un peu de chance -- la plus part du temps -- t'auras un résultats acceptable (ou même bon).

## I get different colors from different (consumer) printers

- printers print differently
- you can you try directly printing a picture (without scribus) on both printer and see if you see the same difference?
- using color management and the matching color profiles could help in getting the same result from both printers, but most consumer printers do not provide the profiles (and they also tend to print with different tones depending on the fill state of the toners)

## The images do not look in print like in Scribus

If you let Scribus resize your images when exporting to PDF, you could have nasty effects in the resulting print (banding, ...)

If you want to keep full control on the way images are printed, you should resize them before loading them into Scribus.

## Scribus does not behave correctly...

In our experience, reinstalling Scribus is not a solution to (almost) any problem.

If Scribus suddenly behaves oddly, there could be three reasons:

- you have changed a setting; 
- the document is corrupted;
- the settings are corrupted.

## Missing Dialogs, Windows or Toolbars

- If a specific dialog does not show:
  - It could be outside of the visible part of the screen:
    - On Windows:
      - Make sure that the dialog is visible and active (as an example by activating it from the menus),
      - Press `alt-space` to show the "Window"-dialog
      - With the keyboard, select the "move" action.
      - Use the keyboard arrows to move around the dialog until it's visible again.
- If a toolbar has disappeared:
  - Right click on the gray area next to another toolbar and re-activate the one that you are missing
- If a toolbar is not where it used to be:
  - Move the toolbar to area where it used to be: slowly move it in small circles until it shows as docked and then release the mouse.

## A corrupted document

## Corrupted settings

If the settings are corrupted you can get Scribus to recreate them.

_Warning_: You will lose your current settings (list of active fonts, visibility of the toolbars, ...) by doing so. If possible, you should first backup your current settings (see below).

### Recreate the settings on Linux

First make sure that Scribus is not running.

In your file manager make sure that you can see the hidden files and directories (hidden files and directories are the ones that start with a dot).

In your home directory, find the `.config` directory. It contains a `scribus` directory you can rename to `scribus~`. Start Scribus and check if your problem is solved. If it's not, you can remove the newly created `.scribus` directory and rename `scribus~` back to `.scribus`.

For 1.4.x:

In your home directory, find the `.scribus` directory and rename it to `scribus~`. Start Scribus and check if your problem is solved. If it's not, you can remove the newly created `.scribus` directory and rename `scribus~` back to `.scribus`.

If you're comfortable with the terminal you can

    $ cd ~/.config
    $ mv -i .scribus scribus~
    $ scribus

If this does not solve your issue

    $ rm -rf .scribus
    $ mv scribus~ .scribus
    $ scribus

## Recreate the settings on Mac OS X

Your settings are in ` ~/Library/Preferences/Scribus/`.  
`~` is your user's directory (mostly `/Users/YourName/`).

You can reach the preference directory by...

Close Scribus and then rename the `Scribus` directory in the user's preferences to `Scribus~` and then restart Scribus.

If this does not solve your issue you can remove the newly created `Scribus` directory and then rename `Scribus~` back to `Scribus`.

## Recreate the settings on Microsoft Windows

On Windows 8 and Windows 10 there is a Scribus directory in the `AppData` directory:

`C:\Users\<username>\AppData\Roaming\Scribus`

For Scribus 1.4, Scribus uses the file `prefs140.xml` (eventually also `scribus140.rc`).  
For 1.5.x the preferences are in `prefs150.xml` (eventually also `scribus150.rc`).

Rename this file to force Scribus to create a fresh one (as it does when you first run it).  
On the next start of Scribus you will get the message:

"Konnte die ... scribus150.rc nicht öffnen. unexpected end of file in Zeile 1 Spalte 1. Es werden die Standardeinstellungen geladen."

Scribus will then create the new settings for you.

# Finding the Scribus resources

Resources like the Scrapbook are in:

- On Linux: `~/.local/share/scribus/`
- On Os X: `/User/<Your user>/Library/Application Support/Scribus/`
- On Windows: `C:\Users\username\AppData\Roaming\Scribus\` (unconfirmed)

## I cannot edit (parts of) my document

- check if you have multiple layers (window > layers) and, if it's the case, you're on the right one and it's not locked.
- check that the items you want to edit are not on a master page.
- check that view > preview > preview mode is not enabled


## When I export to PDF there is nothing

In the layers dialog, make sure that your Layers are "printable".

## I cannot apply "abc" formatting in the Story editor

- n'utilise pas l'éditeur "interne". sauf si tu en as vraiment besoin. (mas c'est rare)
- double clique sur le cadre pour éditer le contenu d'un cadre texte.
- ouvre la palette des propriétés (depuis le menu "fenêtre" et cherche le tab "texte"

## I cannot apply bold / italic

- scribus ne connaît ni gras ni italique. il te faut utiliser la variante gras ou italique de la police (dans la liste des polices...)

## When exporting to Pdf my images get a white background

If your document contains transparencies, when exporting to PDF you will have use a version that supports them.

As an example, pdf 1.4 and pdf 1.5 do support them, but many pdf standards do not support transparencies...

But take care: even if those "newer" standards have been around for a long time, your print shop might not accept them or break them.

## When printing my document, my images get a white background

Don't print directly from Scribus, first create a Pdf and then print it with a (good) Pdf reader.

## Compiling Scribus

- If you get weird errors, try to run `cmake` with the option `-DWANT_NOOSG=1`. It will disable OSG and you will probably never miss it.

## Monitor issues

### Scaling on High DPI displays

#### Windows

According to [Adobe App Scaling on High DPI Displays (FIX)](http://www.danantonielli.com/adobe-app-scaling-on-high-dpi-displays-fix/), you can tell Windows to prefer external manifest and then add a manifest next to the Scribus binary.

One comment to that article and a [Scribus Forum thread](http://forums.scribus.net/index.php/topic,2237.msg12076.html) seem to confirm that this hack does work.

Starting with Scribus 1.5.3 you should probably have no issue anymore with HDPI.

## Enabled features: the C-C-T

- C: LitlleCMS is enabled
- C: Cups is enabled
- T: Tiff support

Remark: On Windows and OS X Cups is not relevant and cannot be enabled.

# Something does not work in Scribus

## Why the Story Editor...?

TLDR: If the Story Editor does not fit your needs, don't use it.

The Story editor is a "leftover" of the good old time, when the in frame editing was not good enough / was too sluggish.

Nowadays, it might be useful in some very specific case, but not for normal editing.
It was there in every layout software.

Sadly, many tutorials present it at the very start and people think it's handy while doing very simple things (it is probably less overwhelming than having to show/hide the palettes and figure out what all those buttons mean... then, when they miss some features, instead of switching to the in frame editing complain that the Story editor is not good enough...)

Anyway, I don't think that there will be any relevant change to the Story editor.
It's dead code.
It has already been for many years.
But it would be nice to have a new editor that focuses on performance of the editing, maybe external to Scribus and enabling multiple users to edit different parts of the Scribus file.

But we need several other improvements to Scribus, before such a tool would really be useful.
So, it's not for the near future.

# Download issues

## Scribus is not a virus / trojan

We sometimes get messages from user affirming that some anti virus tiool flagged the Scribus installer they have downloaded.

If you are sure that you downloaded the correct package by following the links on <https://scribus.net/downloads> and you trust the antivirus tool, then do not install Scribus for now.  
Try in a few days or hours again and see if the package is still flagged.

Do not install Scribus.

This having been said:

- Are you 100% sure that you got the installer from the Sourceforge page linked from <https://scribus.net/downloads>?
- Do you trust you the antivirus or is it a random antivirus you installed from the internet?
  If you're using Windows, you should probably only use the antivirus provided by Microsoft and trust it: it's good enough.
  If it's not your only antivirus or if you don't really trust it, you probably need to reconsider your security choices.
- About twice a year we get reports that Scribus got flagged by one of many tools (often VirusTotal is mentioned).  
  As far as we can tell, the reports were never correct.  
  And nobody is known to ever got a virus from an installer downloaded from the links on the official page.
- If you really want to do something, you should get in touch with the publisher of the antivirus and get them to check if the alert is legit. But it's unlikely that you will ever get a reply.
