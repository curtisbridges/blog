---
title: "Big Nerd Ranch, Beginning iOS - Day 4"
date: 2014-10-16
canonical: ""
description: ""
tags: [iOS, swift]
draft: false
---
Coming off yesterday’s high, I was very much looking forward to today.

<!--more-->

Today started an entirely new project, a home inventory app. This app is designed with a table view, a control used constantly in iOS apps and within iOS itself. Given its widespread use, this is an important day of hands-on training.

I found the control to be interesting but not entirely what I was expecting; I’ve used a lot of table controls in prior UI implementation, but it is a little different on iOS. Most tables have a variable amount of columns as well as rows on other platforms – on iOS it appears that tables have a single column and rows themselves are designed around a single control of your design. This design can include “column-like” structures but aren’t required to look like columns. This makes UITableView something entirely different to me. It certainly allows for some rich display of items but isn’t exactly like a traditional spreadsheet design.

Another interesting aspect of UITableView are the other parts of the control – headers, footers, and even a notion of sections. Christian (the instructor) pointed out how iOS’s Settings app uses sections. This certainly makes for some different takes on the design of an application.

We then learned some CRUD (Create, Read, Update, Delete) operations on tables. iOS does some interesting things when it comes to efficiency of UI display by reusing cells when it can. The rest was pretty typical stuff.

Next, we added a navigation control to our design. This control is fundamental to mobile app design, as it allows a hierarchy of views to be navigated and have a standard “back” button to return from “drill down” views. The drill-down view for our table view of inventory items was a detailed view of an item. This showed name, serial number, value and date created. To this view, we eventually added a toolbar that linked to the camera app using the system’s camera button and eventually made it also allow editing of the photo selected. This detailed item view then displayed the selected photo.

Lastly, we tied the app into system events so our inventory could be persisted to disk. At this point, you have a reasonable app’s functionality. Tomorrow will involve Auto Layout to clean up some of the visual aspects of the app to add a significant amount of polish.

This has been a great experience so far and I truly feel like we’ve gained a a broad spectrum of the core of iOS development already.
