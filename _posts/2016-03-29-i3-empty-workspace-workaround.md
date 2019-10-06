---
layout: post
title: "Empty workspace in I3 WM"
description: "A workaround to having an empty workspace without it disappearing"
tag:
  - i3-wm
---

When using [I3 window manager](https://i3wm.org/), one cannot have an empty [workspace](http://i3wm.org/docs/userguide.html#_using_workspaces). As soon as you switch to another workspace, the empty workspace disappers. As there is no special 'destroy' command to delete workspaces, this is the way I3 deals with removing and recycling workspaces. Using the [layout saving](http://i3wm.org/docs/layout-saving.html) functionality, I may have found a way to have an empty workspace.  

First of all, take a look at the following I3 layout file:

~~~json
{
  "border": "pixel",
  "floating": "auto_off",
  "layout": "stacked",
  "percent": 1,
  "type": "con",
  "nodes": [
    {
      "border": "pixel",
      "current_border_width": 3,
      "floating": "auto_off",
      "geometry": {
        "height": 523,
        "width": 802,
        "x": 0,
        "y": 0
      },
      "name": "",
      "percent": null,
      "swallows": [
        {
          "class": ".*"
        }
      ],
      "type": "con"
    }
  ]
}
~~~

When you apply this layout to a workspace by executing `i3-msg 'append_layout empty_workspace.json'`, it will create a container which will _eat_ any window that gets created next. Notice the `"class":".*"` line; this matches any program. Now, if we create a new workspace and then apply this layout, we can switch to another workspace without the fear of the new workspace disappearing.

Given a workspace name, the following bash script checks if the workspace exists, and if it does, switches to it; If the workspace doesn't exist, then it creates the workspace and applies the above mentioned layout.

~~~sh
WKNAME=$1
echo workspace name given is $WKNAME
if i3-msg -t get_workspaces | jq ".[] | .name" | grep -q -w $WKNAME; then
  i3-msg "workspace $WKNAME"
else
  i3-msg "workspace $WKNAME; append_layout ~/.i3/empty_workspace.json"
fi
~~~~

But what about the case when we delete all the windows in a workspace, and then switch to another workspace? The workspace will still get destroyed in that case. We can write another script which takes care of this case:

~~~sh
currentDesk=$(xdotool get_desktop)
awkArgs="'\$2 == \"$currentDesk\" {print \$3}'"
getNumWindows="wmctrl -l | awk ${awkArgs} | wc -l"
numWindows=`eval $getNumWindows`

echo $numWindows
if ((numWindows > 1)); then
  i3-msg "kill"
else 
  i3-msg "kill; append_layout ~/.i3/empty_workspace.json"
fi
~~~

This scripts checks if the current window is the last remaining window in the current workspace, and if it is, then applies the empty_workspace.json layout after killing the window. Using these two bash scripts and the layout file, we can have a empty workspace and not let it get destroyed.

