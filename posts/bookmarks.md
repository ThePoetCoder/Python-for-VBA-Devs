# Using Bookmarks

To be completely honest, I prefer the way the VBE handles bookmarks rather than PyCharm. Even with tweaking the environment it's difficult to bring back the functionality found in the VBE. In fact I rarely use the bookmarks feature in PyCharm for this reason, whereas I used it all the time in the VBE, but I actually manage to get by without it nicely with a handful of other code naviagation techniques. But if you are so inclined, at the end of this post I will walk you through getting PyCharm as close as possible to recreating the bookmark buttons in the VBE.

The main problem is that even though PyCharm can *track* bookmarks across the scope of an entire project, it cannot jump back and forth between bookmarks outside of the currently open document as easily. The only way to get close is to use numbered mnemonics with your bookmarks, which could be of use to you, I just don't like it as much personally, but we'll go over in this post nonetheless. So if you're writing code that interacts with multiple files/modules (which is relatively often) you'll have to either use a mnemonic-bookmark, use the "Bookmarks" popup window, or make more use out of the following code navigation keyboard shortcuts:

* The keyboard shortcut `CTRL + B` - This is PyCharm's version of the VBE's keyboard shortcut `Shift + F2`, both of which will take you wherever in the codebase the variable you're working with is defined. PyCharm's version is especially powerful in that you can jump into code you didn't write, such as the Python source code or a library you're learning how to use.

* The keyboard shortcut `CTRL + Shift + F` - This is my preferred way (out of the multiple different ways available in PyCharm) to search for text across the entire scope of the project (and you can change the scope right within the window, just like the VBE). In my opinion PyCharm's tool is much more useful than the VBE's in that it displays all your results at once inside the popup window instead of jumping your position one by one throughout the codebase. You can choose to jump if you wish by double clicking on any item, but you can also edit code right inside the popup window and have it immediately edited in the original file as well.

If you are stubborn though and want to get as close to the functionality of the VBE as possible, here is what to do:
1. Save the following images to your computer:
* ![Show Bookmarks](../images/Show_Bookmarks.png) - Show Bookmarks
* ![Toggle Bookmark](../images/Toggle_Bookmark.png) - Toggle Bookmark
* ![Next Bookmark](../images/Next_Bookmark.png) - Next Bookmark
* ![Previous Bookmark](../images/Previous_Bookmark.png) - Previous Bookmark
2. Open PyCharm
3. Click on the "Settings" icon (looks like a wrench) or click through "File > Settings".
4. In the Settings popup window click "Appearance and Behavior > Menus and Toolbars > Main Toolbar"
5. Find a place on the main toolbar you'd like to add some bookmark related buttons. I put mine right above (which on the toolbar is to the left) of the "Toolbar Run Actions".
6. Click on the "+" icon above and select "Add Separator". It will add it below the item you have selected.
7. Click on the "+" icon above and select "Add Action..." this time.
8. In the "Choose Actions to Add" popup that comes up, type in the word "Bookmark" to quickly find the folder labeled "Bookmarks" and open it.
9. Click on one of the actions.
10. Set the icon to match the icons I've added above (you can click on the folder at the bottom of the "Choose Actions to Add" popup to browse for the images.
11. Select "Ok"
12. Repeat steps 7-11 for each of the four buttons found in the VBE.

You should now have something that looks very familiar to you. The "Show Bookmarks" button is new obviously, as PyCharm makes more use out of this popup window when finding bookmarks than simply jumping to the next one sequentially. You can toggle a line to be bookmarked with the "Toggle Bookmark" button now, or by hitting F11. Every time you add a bookmark anywhere in the project, it will show up on the "Bookmarks" popup window.

If you wish to use a mnemonic with your bookmark, you can use the keyboard shortcut "CTRL + F11" and select a number or letter to distinguish this bookmarks from others. If you chose a number, from then on, anywhere in your project you can hit "CTRL + {{your number}}" to jump to that bookmark, which is actually very handy. Unfortunately this does not work the same way if you choose a letter for your mnemonic, but you can instead click on the bookmark itself to the left of your code and use the "Edit Bookmark Description..." feature to change the words that appear next to the bookmark in the "Bookmarks" window to more easily find it among however many other bookmarks you add.
