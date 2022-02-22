> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [docs.kde.org](https://docs.kde.org/stable5/en/konsole/konsole/commandreference.html#menubar)

> The menubar is at the top of the Konsole window. If the menubar is hidden, can be reached by right c......

The menubar is at the top of the Konsole window. If the menubar is hidden, can be reached by right clicking in the window (as long as no full screen application is running in that window such as vi, minicom, etc.). The default shortcut is listed after each menu item.

Alternatively you can use the shortcut **Ctrl**+**Shift**+**M** to show or hide the menubar.

→ (****Ctrl**+**Shift**+**N****)

Opens a new separate Konsole window with the default profile

→ (****Ctrl**+**Shift**+**T****)

Opens a new tab with the default profile

### Note

The first profile in the submenu will always be "Default" which is the built-in profile. All other profiles will be listed below that in alphabetical order. The user specified default profile will be in bold type.

→

Attempts to clone the current tab in a new tab

→ (****Ctrl**+**Shift**+**S****)

Saves the current scrollback as a text or html file

→ (****Ctrl**+**Shift**+**P****)

Print the current screen. By default the output is scaled to fit the size of the paper being printed on with black text color and no background. In the print dialog these options can be changed on the Output Options tab.

→

Opens KDE's file manager at the current directory. By default, that is [Dolphin](https://docs.kde.org/?branch=stable5&language=en&application=dolphin&path=index.html).

→ (****Ctrl**+**Shift**+**W****)

Closes the current session

→ (****Ctrl**+**Shift**+**Q****)

Quits Konsole

### Note

Konsole will display a confirmation dialog if there is more than one session open or if there are certain programs running in any session. These dialogs can be disabled by clicking on the Do not ask again checkbox.

→ (****Ctrl**+**Shift**+**C****)

Copies the selected text to the clipboard

→ (****Ctrl**+**Shift**+**V****)

Pastes text from the clipboard at the cursor location

→

Selects all the text in current window

→ →

Allows input from the current session to be sent simultaneously to all sessions in current window

→ → (****Ctrl**+**Shift**+**.****)

Allows input from the current session to be sent simultaneously to sessions picked by user

→ → (****Ctrl**+**Shift**+**/****)

Stop sending input from current session into other sessions

→

Send the specified signal to the shell process, or other process, that was launched when the new session was started.

Currently available signals are:

<table><colgroup><col><col></colgroup><tbody><tr><td>STOP</td><td>to stop process</td></tr><tr><td>CONT</td><td>continue if stopped</td></tr><tr><td>HUP</td><td>hangup detected on controlling terminal, or death of controlling process</td></tr><tr><td>INT</td><td>interrupt from keyboard</td></tr><tr><td>TERM</td><td>termination signal</td></tr><tr><td>KILL</td><td>kill signal</td></tr><tr><td>USR1</td><td>user signal 1</td></tr><tr><td>USR2</td><td>user signal 2</td></tr></tbody></table>

Refer to your system manual pages for further details by giving the command **``**man** `7 signal` ``**.

→ (****Ctrl**+**Alt**+**S****)

Opens a dialog box allowing you to change the name format, the remote tab title format and the color of the current tab ([more info](https://docs.kde.org/stable5/en/konsole/konsole/console-dialogs.html#configure-tab-settings-dialog "Configure Tab Settings Dialog"))

→ (****Ctrl**+**Alt**+**U****)

Opens up a dialog to select a file to be uploaded if the required software is installed

→ (****Ctrl**+**Shift**+**F****)

Opens a search bar at the bottom of Konsole's window

This allows for case sensitive, forward or backwards, and regular expressions searches.

→ (****F3****)

Moves to the next search instance . If the search bar has the focus, you can use the shortcut Enter as well.

→ (****Shift**+**F3****)

Moves to the previous search instance . If the search bar has the focus, you can use the shortcut **Shift**+Enter as well.

→ → (****Ctrl**+**(****)

Splits all the tabs into left and right views

Any output on one view is duplicated in the other view.

→ → (****Ctrl**+**)****)

Splits all the tabs into top and bottom views

Any output on one view is duplicated in the other view.

→ → (****Ctrl**+**Shift**+**]****)

Makes the current view larger

→ → (****Ctrl**+**Shift**+**[****)

Makes the current view smaller

→ → (****Ctrl**+**Shift**+**E****)

Toggles the current view between current size and the maximize size

→ (****Ctrl**+**Shift**+**L****)

Opens the current tab in a separate window

Quitting the previous Konsole window will not affect the newly created window.

→ (****Ctrl**+**Shift**+**H****)

Opens the current split view in a separate window

→

Allows you to save the tab layout of the current view in a specialized Konsole layout file which can then be loaded to restore one of your favorite layouts.

→

Allows you to load one of your favorite view layouts from the layout file that has been saved using the → menu item earlier. The default layouts (2x2, 2x1, and 1x2) can be loaded via toolbar.

→ (****Ctrl**+**Shift**+**I****)

Toggles the monitoring of the current tab for lack of activity

By default, after 10 seconds of inactivity, an info icon will appear on the session's tab. The type of alerts can be changed through → → .

→ (****Ctrl**+**Shift**+**A****)

Toggles the monitoring of the current tab for activity

Upon any activity, an info icon will appear on the session's tab. The type of alerts can be changed through → → .

→

Toggles the monitoring of the current tab for the process finishing.

If checked, upon finishing the current process, Konsole will show a notification The process '_`name of the process`_'has finished running in session'_`name of the session`_'.

→

Toggles the session to be read-only: no input is accepted, drag and drop is disabled.

→ (****Ctrl**+**+****)

Increases the text font size

→ (****Ctrl**+**0****)

Reset the text font size to the profile default

→ (****Ctrl**+**-****)

Decreases the text font size

→

Sets the character encoding

→

Clears the text in the scrollback

→ (****Ctrl**+**Shift**+**K****)

Clears the text in the current tab and scrollback and resets the terminal

→ (****F11****)

Toggles Konsole filling the entire screen

→ (****Ctrl**+**Shift**+**B****)

Adds the current location

→

Adds all tabs to a bookmark folder

A dialog will open for the bookmark folder name.

→

Adds a new folder to the bookmark list

A dialog will open for the bookmark folder name.

→

Opens the bookmark editor

### Note

The keditbookmarks program must be installed for this menu item to appear.

You can use the bookmark editor to manually add URLs. Currently, Konsole accepts the following:

*   ssh://user@host:port
    
*   telnet://user@host:port
    

Any installed plugins will be listed or "No plugins available"

→

Opens a dialog to configure current profile

→

Switch current profile to a listed profile

→

Opens an editor for managing profiles

→

Change Konsole's GUI to the specified scheme

→ (****Ctrl**+**Shift**+**M****)

Toggles the menubar being visible

→

Allows visibility toggling of the Konsole toolbars

→

Toggles the statusbar being visible

→

Opens window to choose an interface translation of Konsole.

→

Opens the keyboard shortcut editor. More on shortcuts configuration can be found in the [KDE Fundamentals](https://docs.kde.org/?branch=stable5&language=en&application=fundamentals&path=shortcuts.html).

Additionally Konsole has a few special shortcuts with no corresponding menu item:

<table><colgroup><col><col></colgroup><thead><tr><th>Shortcut</th><th>Description</th></tr></thead><tbody><tr><td><strong>Shift</strong>+Right</td><td>Next Tab</td></tr><tr><td><strong>Shift</strong>+Left</td><td>Previous Tab</td></tr><tr><td><strong>Ctrl</strong>+<strong>Alt</strong>+Left</td><td>Move Tab Left</td></tr><tr><td><strong>Ctrl</strong>+<strong>Alt</strong>+Right</td><td>Move Tab Right</td></tr><tr><td><strong>Ctrl</strong>+<strong>Shift</strong>+Ins</td><td>Paste Selection</td></tr></tbody></table>

→

Opens [the toolbar configuration window](https://docs.kde.org/?branch=stable5&language=en&application=fundamentals&path=config.html#toolbars-items)

→

Opens the notifications editor

→

Opens the Konsole settings editor

This dialog has options influencing the appearance and behaviour of the Konsole window.

*   The General page allows configuring the menubar visibility, remembering the Konsole window size, running all Konsole windows in a single process, enabling menu accelerators, showing window title on the titlebar, removing window titlebar and frame, and focusing terminals when the mouse pointer is moved over them. It is also possible to configure the search case sensitivity, usage of the regular expression, highlighting all matches, and the search direction (Search backwards is the default). The General page is also the place where you can Enable all "Don't Ask Again" messages again if they were switched off before.
    
*   The Profiles page is meant for creating and handling [profiles](https://docs.kde.org/stable5/en/konsole/konsole/profiles.html "Profiles").
    
*   Using the Tab Bar/Splitters page you can configure the visibility and placement of tab bar, define tabs behavior and fine-tune the tab buttons options. It is possible to configure if you want to Show 'New Tab' button and Expand individual tab widths to full window or configure Use user-defined stylesheet. The Behavior tab can be used to define the place for the new tabs (At the end or After current tab) and closing of tabs with a middle mouse button click.
    
    It is also possible to configure visibility of the split headers (When needed (default), Always, or Never) and define the drag handle size for splits (Small (default), Medium, or Large) using the Splits tab of this configuration page.
    
*   The Temporary Files page is used to define the [scrollback](https://docs.kde.org/stable5/en/konsole/konsole/scrollback.html "Scrollback") file location.
    
*   The Thumbnails page can be used to define the thumbnail size and activation options (you can choose the activation control key from **Shift**, **Alt**, and **Ctrl**).
    
    ### Note
    
    To use the thumbnails feature showing image thumbnails in popups when hovering image items with the mouse pointer, you should enable file underlining for your current profile: → → → → .
    

Konsole has the some of the common KDE menu items, for more information read the section about the [Help Menu](https://docs.kde.org/?branch=stable5&language=en&application=fundamentals&path=menus.html#menus-help) of the KDE Fundamentals.