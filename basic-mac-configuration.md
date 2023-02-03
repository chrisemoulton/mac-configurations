## <a name='toc'>Table of Contents</a>
- [ ] [Use apps in Split View on Mac](#split):
- [ ] [copy full path in mac](#copypath):
- [ ] [Create text file at any location in finder app](#textfile):
- [ ] [Adding application to finder window](#addAppFinder):
- [ ] [Image editing tool](#imageEditingTool):
- [ ] [Control audio based on application](#audioControl):
- [ ] [Solution to "application is damaged and move it bin](#appdamaged):




#### [[⬆]](#toc) <a name='split'>Use apps in Split View on Mac</a>

https://support.apple.com/en-in/guide/mac-help/use-apps-in-split-view-mchl4fbe2921/10.14/mac/10.14

Many apps on your Mac support Split View mode, where you can work in two apps side by side at the same time.

Two apps side by side in Split View.
On your Mac, in the top-left corner of an app window, click and hold the green button, drag the window to the side you want, then release the button.

The button to click for entering full screen.
On the other side of the screen, click the second app you want to work with.

In Split View, do any of the following:

Make one side bigger: Move the pointer over the separator bar located in the middle, then drag it left or right. To return to the original sizes, double-click the separator bar.

Change sides: Use a window’s toolbar to drag the window to the other side. If you don’t see a toolbar, click the window, then move the pointer to the top of the screen.

Show or hide the menu bar: Move the pointer to or away from the top of the screen.

Show or hide the Dock: Move the pointer to or away from the Dock’s location.

To stop using an app in Split View, click its window, show the menu bar, then click the green button in the window’s top-left corner or press Control-Command-F.  
The remaining app expands to full screen and can be accessed in the Spaces bar. To stop using the app full screen, move the pointer over its thumbnail in the Spaces bar,  
then click the Exit button  that appears in the top-left corner of the thumbnail.

If you’re using an app full screen, you can quickly choose another app to work with in Split View. 
Press Control-Up Arrow (or swipe up with three or four fingers) to enter Mission Control, then drag a window from Mission Control onto the thumbnail of the full-screen app in the Spaces bar.  
You can also drag one app thumbnail onto another in the Spaces bar.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### [[⬆]](#toc) <a name='copypath'>copy full path in mac</a>

http://osxdaily.com/2013/06/19/copy-file-folder-path-mac-os-x/

[Workflow](https://github.com/dineshbhagat/mac-configurations/blob/main/images/Copy%20Path.workflow.zip)


For **MacOS Big sur**: 
1. https://macosxautomation.com/automator/services/

OR

1. Select a file or folder and perform a right-click.  
2. When the context menu pops up, press and hold the Option key on the keyboard.  
3. Copy “file-name” as Pathname option will appear in the context menu. Just click it to copy the full file path to the clipboard.  

OR  
[Workflow-quickAction](https://github.com/dineshbhagat/mac-configurations/blob/778c16b18e2c5ba3e69ba1e6490ee88c7f1bcd9b/images/copy-path-for-bigsur.zip)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### [[⬆]](#toc) <a name='textfile'>Create text file at any location in finder app</a>

https://github.com/dineshbhagat/mac-configurations/blob/main/images/New%20text%20File.workflow.zip


Ref: https://zeldor.biz/2017/12/mac-os-x-finder-new-file/

01. Open Automator and create a Service.  
02. Set the input to no input, and the application to Finder.app   
03. Drag and Drop the Run AppleScript workflow element onto the grey space  
04. Put the contents of this AppleScript in the textbox  
05. Save the workflow with a reasonable name (like: New text File)  
06. Go to Settings -> Keyboard -> Shortcuts -> Services and assign a shortcut to it.  

```applescript
set file_name to "untitled"
set file_ext to ".txt"
set is_desktop to false

-- get folder path and if we are in desktop (no folder opened)
try
	tell application "Finder"
		set this_folder to (folder of the front Finder window) as alias
	end tell
on error
	-- no open folder windows
	set this_folder to path to desktop folder as alias
	set is_desktop to true
end try

-- get the new file name (do not override an already existing file)
tell application "System Events"
	set file_list to get the name of every disk item of this_folder
end tell
set new_file to file_name & file_ext
set x to 1
repeat
	if new_file is in file_list then
		set new_file to file_name & " " & x & file_ext
		set x to x + 1
	else
		exit repeat
	end if
end repeat

-- create and select the new file
tell application "Finder"
	
	activate
	set the_file to make new file at folder this_folder with properties {name:new_file}
	if is_desktop is false then
		reveal the_file
	else
		select window of desktop
		set selection to the_file
		delay 0.1
	end if
end tell

-- press enter (rename)
tell application "System Events"
	tell process "Finder"
		keystroke return
	end tell
end tell
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### [[⬆]](#toc) <a name='addAppFinder'>Adding application to finder window</a>
1. go to folder where application is present in finder e.g. /Applications/
2. Select application, Press command button and drag application to finder toolbar
3. Your screen will look like as below
![image](https://github.com/dineshbhagat/mac-configurations/blob/1598c54473844720d4685ec74d2f1f34b5f24bc9/images/finder-toolbar-customization.png)


https://github.com/dineshbhagat/mac-configurations/blob/main/images/New%20Text%20File.app.zip

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### [[⬆]](#toc) <a name='imageEditingTool'>Append Images using ImageMagick</a>

```bash
brew install ImageMagick;

convert -append ~/Desktop/Screenshot\ 2020-08-11\ at\ 3.03.52\ PM.png ~/Desktop/Screenshot\ 2020-08-11\ at\ 3.06.01\ PM.png  ~/Desktop/out.png
```

------

#### [[⬆]](#toc) <a name='audioControl'> Control audio per application level </a>

```bash
brew cask install background-music
```

Ref: https://github.com/kyleneideck/BackgroundMusic

In case if you see, there is no impact of changing the audio by changing slider ![image](https://github.com/dineshbhagat/mac-configurations/blob/1598c54473844720d4685ec74d2f1f34b5f24bc9/images/backgroundmusic.png)

Then check for audio setting and choose background music option as shown ![image](https://github.com/dineshbhagat/mac-configurations/blob/1598c54473844720d4685ec74d2f1f34b5f24bc9/images/zoom-setting.png)


------

#### [[⬆]](#toc) <a name='appdamaged'> fix-app-damaged-cant-be-opened-trash-error-mac </a>

```bash
xattr -cr /Applications/Signal.app
```

Ref: https://osxdaily.com/2019/02/13/fix-app-damaged-cant-be-opened-trash-error-mac/

------
