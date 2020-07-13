# Regexer SOP

A node that combines the functionallity of all the different regular expression functions in vex (re functions) all wrapped up in a single, easy to use SOP.

Note: As of right now the tool only works on either points or primitives as these were the use cases I needed it for, but if there are any requests for it, I would not mind expanding it to work with detail and vertex attributes in the future.

## Installation

To install this otl all you have to do is download it and place it in one of these folders:

Windows: C:\Program Files\Side Effects Software\Houdini xx.x.xxx\houdini\otls

Mac: /Applications/Houdini/Houdinixx.x.xxx/houdini/otls

Linux: /opt/hfsxx.x.xxx/houdini/otls

After restarting houdini the node should be avalible to place down in SOPs.
It can be found either by right clicking and hovering over the "digital assets" category or by searching for "regexer".

## Usage

### General

**Group Settings** - These are your standard houdini group settings to control what geometry the node should run over.

**Run Over** - Choose where the attribute you want to work with is stored, on points or on primitives.

**Mode** - Currently there are two modes, "Deletion" and "String Processing". "Deletion" allows you to input parameters and automatically blast away geometry based on the results. This was done because often times when I was doing this kind of string processing I was going to delete geo either way, so building it in saves alot of time. "String Processing" allows you to breakdown, split up or keep parts one of your string attributes. 

**Regex Command** - This allows you too choose what command you want to run, note that there are more avalible commands in the string processing section than in the delete section. For a better overview of what each command does have a look [here](https://www.sidefx.com/docs/houdini/vex/functions/re_find.html) (Look for the different commands at the bottom of the page or on the let hand overview).
However, most of the commands do exactly what it sounds like they do, so reading the entire documentation is probably not needed.

**Expression** - Think of this as your search term (what the documentation calls "regex"). This is the term you'd want to search for in your attribute. Say you have a name attribute that goes like this "Red_Point_01", "Blue_Point_01", "Green_Point_01" etc. And you'd like to only keep the points with the name "Red_Point" in it (assuming in this case that there are no other attributes like color to work from), in the "Expression" tab you would input "Red_Point" since you are looking for points with that in their names.

**Attribute to search** - The name of the attribute you would like to search over. Using the naming example again, assuming the name of this attribute would be "name", you would simply put "name" in the "Attributes to search" field, **do not add an @ infront of the attribute name**

**Start Position** - Indicates where to start the search in the string. By using a value of 0 the node will look through the whole string attribute, but by for example setting it to 5, the node will skip the first 5 letters of the string attribute, then start looking.

**Invert** - Inverts the results of the node. So if you searched for "Red_Points" it would return you all the nodes that does **_not_** have "Red_Point" in their name.

### Deletion Mode specific

**Delete Prims/Points** - When using the deleteion mode this toggle will let you delete additional degenerate geometry which might still be remaining. When running over points and deleting points with this node without this checked on, all the primitives might still be there, just with no points attached to them, making them degenerate, use this to remove these too. The same goes for points when running over primitives. If you dont have this checked on it is recommended that you inspect your geometry before and after this node to make sure it seems reasonable or if there are alot of remaining geometry that should not be there.

### String Processing Mode specific

**Output attribute** - This is where the result of the string processing will be stored. It will write it out to a new attribute with the name you choose here. Some of these will be normal strings and some will give you an array.