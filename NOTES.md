# Troubleshooting

## Scribus does not behave correctly

In our experience, reinstalling Scribus is not a solution to (almost) any problem.

If Scribus suddenly behaves oddly, there could be three reasons:

- you have changed a setting; 
- the document is corrupted;
- the settings are corrupted.

### A wrong setting

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

### A corrupted document

### Corrupted settings

If the settings are corrupted you can get Scribus to recreate them.

_Warning_: You will lose your current settings (list of active fonts, visibility of the toolbars, ...) by doing so. If possible, you should first backup your current settings (see below).

#### Recreate the settings on Linux

First make sure that Scribus is not running.

In your file manager make sure that you can see the hidden files and directories (hidden files and directories are the ones that start with a dot).

In your home directory, find the `.scribus` directory and rename it to `scribus~`. Start Scribus and check if your problem is solved. If it's not, you can remove the newly created `.scribus` directory and rename `scribus~` back to `.scribus`.

If you're comfortable with the terminal you can

    $ cd
    $ mv -i .scribus scribus~
    $ scribus

If this does not solve your issue

    $ rm -rf .scribus
    $ mv scribus~ .scribus
    $ scribus

### Recreate the settings on Mac OS X

Your settings are in ` ~/Library/Preferences/Scribus/`.  
`~` is your user's directory (mostly `/Users/YourName/`).

You can reach the preference directory by...

Close Scribus and then rename the `Scribus` directory in the user's preferences to `Scribus~` and then restart Scribus.

If this does not solve your issue you can remove the newly created `Scribus` directory and then rename `Scribus~` back to `Scribus`.

### Recreate the settings on Microsoft Windows

