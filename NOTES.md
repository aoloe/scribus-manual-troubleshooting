# Troubleshooting

What can you do when Scribus does not behave correctly?

Warning: it's very likely that it's not a good idea to create this document. Probably, we will move the content to each specific manual in a "Troubleshooting" chapter.


## Missing fonts

Jean says : In any case you will have to reset font prefences by deleting the checkfonts.xml and
scribus150.rc files stored in preference folder, usually
C:\Users\username\AppData\Roaming\Scribus.

### Missing DejaVu

As of January 2017, Debian testing and Ubuntu 16.04/16.10 are distributing a version of the `freetype` library (2.6.3) that is affected by a bug that prevents Scribus from loading outlines of some glyphs with the DejaVu font (and others).

Freetype 2.6.5 contains a fix for this issue. The fix might already be in the 2.6.4 version.

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

On Windows 8 and Windows 10 there is a Scribus directory in the `AppData` directory.

The prefs140.xml file probably is in `C:\Users\<username>\AppData\Roaming\Scribus`.  
Rename this file to force Scribus to create a fresh one (as it does when you first run it).

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
