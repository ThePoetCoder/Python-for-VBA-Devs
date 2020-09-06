# Bookmarks

To be completely honest, I prefer the way the VBE handles bookmarks rather than PyCharm. Even with tweaking the environment it's difficult to bring back the functionality found in the VBE. In fact I rarely use the bookmarks feature in PyCharm for this reason, and actually manage to get by without it nicely with a handful of other position changing techniques. But if you are so inclined, at the end of this post I will walk you through getting PyCharm as close as possible to using the bookmark buttons in the VBE.

The main problem is that even though PyCharm can *track* bookmarks across the scope of an entire project, it cannot jump back and forth between bookmarks outside of the currently open document. So if you're writing code that interacts with multiple files/modules (which is relatively often) you'll have to either use a bookmark GUI or make more use out of the following:

* The keyboard shortcut `CTRL + B` - This is PyCharm's version of the VBE's keyboard shortcut `Shift + F2`, both of which will take you wherever in the codebase the variable you're working with is defined. PyCharm's version is especially powerful in that you can jump into code you didn't write, such as the Python source code or a library you're learning how to use.

* The keyboard shortcut `CTRL + Shift + F` - This is ny preferred way (out of the multiple different ways available in PyCharm) to search for text across the entire scope of the project. In my opinion PyCharm's tool is much more useful than the VBE's in that it displays all your results at once inside the popup window instead of jumping your position one by one throughout the codebase. You can choose to jump if you wish by double clicking on any item, but you can also edit code right inside the popup window and have it immediately edited in the original file as well.

If you are stubborn and want to get as close to the functionality of the VBE as possible, here is what to do:
1. Open PyCharm
2. Click on the "Settings" icon (looks like a wrench) or click through "File > Settings".
3. In the Settings popup window click "Appearance and Behavior > Menus and Toolbars > Main Toolbar"
4. Find a place on the main toolbar you'd like to add some bookmark related buttons. I put mine right above (which on the toolbar is to the left) of the "Toolbar Run Actions".
5. Click on the "+" icon above and select "Add Separator"
6. 
