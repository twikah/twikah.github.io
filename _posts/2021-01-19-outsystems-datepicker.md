---
postHero: /images/calendar.png
title: 'OutSystems - Implementing the Date Picker widget in Mobile and Reactive apps (Part 1)'
categories: work
tags: [web-development, outsystems, service-studio]
---

This is a how-to guide on how to implement the OutSystems’ built-in Date Picker
widget and override some undesired behaviour on the way.

<br>

I’m working on a project where, a while ago, I needed to identify all the
existing Input widgets that had the data type set to “Date” to replace them with
the OutSystems’ built-in Date Picker widget.

<br>

Once I started implementing the new Date Picker widget, I faced some challenges:

&nbsp;&nbsp;&nbsp;&nbsp; 1. I wanted to set the **date format** as "DD/MM/YYYY"
but the dates would show as "YYYY-MM-DD";

&nbsp;&nbsp;&nbsp;&nbsp; 2. The Date Picker is bound to an Input widget which
shows the selected date. The Input widget **allowed the user to write on it**,
whether it already had a date selected or not;

&nbsp;&nbsp;&nbsp;&nbsp; 3. The Input widget mentioned above (which is inside a
form) was **not** set to mandatory - meaning that I should be able to save a
record without setting the date on it. From here, 3 scenarios emerged:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.1. I didn't select any date on
the Date Picker and everything went well.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.2. I selected a date on the
Date Picker and then I hit delete to remove that date. Then, I saved the record
and **the date that I tried to delete was still persisted on the database**.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.3. Instead of directly hitting
the delete key to remove the date, I selected the date with my mouse and hit
delete afterwards. Then, I saved the record and this time I was able to save the
record with a null date.

<br>

I created a little video demonstrating the odd behaviour outlined in point 3
above.

<br>

<div style="height: 0; padding-bottom: calc(56.25%); position:relative;
width: 100%;">
  <iframe allow="autoplay; gyroscope;" allowfullscreen height="100%"
referrerpolicy="strict-origin" src="https://www.kapwing.com/e/600cbb5f9e67890046d4914a"
style="border:0; height:100%; left:0; overflow:hidden; position:absolute; top:0; width:100%"
title="Embedded content made on Kapwing" width="100%">
  </iframe>
</div>

<p style="font-size: 12px; text-align: right;">
  Content made on <a href="https://www.kapwing.com/videos/600cbb5f9e67890046d4914a"
  target="_blank" rel="noopener noreferrer">Kapwing</a>
</p>

<br>

I searched the OutSystems documentation, the forums and the OutSystems UI Style
Guide for solutions. This post acts as a *how-to guide* to set the Date Picker
to behave in the best possible way.

<br>

The guide will be lengthy so I'll split it into 2 parts. Part 1 details how I
set up the widget and sorted the date format issue. Part 2 will show what I did
to overcome points 2 and 3 from the list above.

<br>

I'll be using a Reactive app to illustrate each step. The user story is **I want
my users to be able to book a vacation period**. The following screenshots are
from the screen *VacationCreation*, where there's a form to accomplish my goal.

<br>

Here's what I did:

&nbsp;&nbsp;&nbsp;&nbsp; 1. I created a local variable for each Date Picker on
the screen. In my *VacationPlanner* app, I needed a **Start Date input** and
**End Date input** to book my vacations. I named these local variables
*PickedBookingStartDate* and *PickedBookingEndDate*. Both have the data type
"Text";

<br>
<div class="center-img">
  <img class="img-medium" src="/images/os_datepicker-1.png"
  alt="Setting up local variables">
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 2. I set the variable property of the Inputs (to which
the Date Pickers are bound) to the local variables created above. I changed
their data type to "Text" as well;

<br>
<div class="center-img">
  <img src="/images/os_datepicker-2.png"
  alt="Assigning the local variable PickedBookingStartDate to the Input’s variable property">
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 3. If the user is editing an existing vacation booking,
I want to display any dates previously saved. For that, I needed to assign the
variables created on step 1 to any existing date on my booking. I selected the
aggregate *GetBookingbyId*  -  which is used to record and populate the fields
on my screen  -  and added a **new action to its On After Fetch event**;

<br>
<div class="center-img">
  <img class="img-medium" src="/images/os_datepicker-3.png"
  alt="Adding an action to the GetBookingById’s On After Fetch event">
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 4. On my action *GetBookingByIdOnAfterFetch*, I
assigned the dates from the database to their corresponding local variables
from step 1. Here, I checked if the saved dates were null dates and, if not, I
converted them into text;

<br>
<div class="center-img">
  <img class="img-large" src="/images/os_datepicker-4.png"
  alt="Getting any existing DB values with On After Fetch action">
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 5. I added the desired **date format** to the Date
Picker's DateFormat property;

<br>
<div class="center-img">
  <img src="/images/os_datepicker-5.png"
  alt="Setting the Date Picker’s date format">
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 6. I set the OnSelect handler of the Date Pickers to
their corresponding actions. Each picker has its own handler action - 
*OnSelectDate_StartDate* and *OnSelectDate_EndDate*;

<br>
<div class="center-img">
  <img class="img-large" src="/images/os_datepicker-6.png"
  alt="Setting the Date Picker’s OnSelect handlers">
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 7. To be able to save the new selected dates, I added
the following assign on my *CreateEditBooking* action:

<br>
<div class="center-img">
  <img class="img-large" src="/images/os_datepicker-7.png"
  alt="Saving the Date Picker’s dates">
</div>
<br>

And that's how I sorted the issue with the date format.

Check out Part 2 of this guide to see how I tackled points 2 and 3 from the list!


