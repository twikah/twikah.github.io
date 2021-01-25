---
postHero: /images/calendar.png
title: 'OutSystems - Implementing the Date Picker widget in Mobile and Reactive apps (Part 2)'
categories: work
tags: [web-development, outsystems, service-studio]
---

This is the Part 2 of a how-to guide on how to implement the OutSystems’
built-in Date Picker widget and override some undesired behaviour on the way.

<br>

On [Part 1](https://twikah.github.io/work/2021/01/19/outsystems-datepicker-pt1.html)
of this guide, I handled the Date Picker set up and fixed an issue with its
date format. Now, I’ll show you how I sorted the issues of:

&nbsp;&nbsp;&nbsp;&nbsp; - Being able to write on an Input bound to a Date Picker
**(point 2 from Part 1)**, and;

&nbsp;&nbsp;&nbsp;&nbsp; - How to remove a date from a Date Picker
**(point 3 from Part 1)**;

<br>

To tackle these points, I added a snippet of javascript to the code. The idea is
to add the JS snippet when the page is ready, to **(point 2) prevent the user
from typing on the Input widget** and **(point 3) to call a new action if the
user clicks on delete**. This new action **forces the local variable to be
assigned to a null date whenever the user clicks on delete**.

<br>

On the snippet below, I added a **listener to each Date Picker and corresponding
input container** to call the action *DatePickerOnSelect_DeleteStart* or
*DatePickerOnSelect_DeleteEnd* if the user clicked on the delete key (keyCode 46)
and to also prevent the default behaviour on the Input widgets and thus
preventing the user from typing anything on those inputs.

<br>

```css
$("#" + $parameters.StartContainerId + ".DatePickerInput").on("keydown", function(event) {
  if (event.keyCode === 46 ) {
    $actions.DatePickerOnSelect_DeleteStart();
  }
  event.preventDefault();
});

$("#" + $parameters.EndContainerId + ".DatePickerInput").on("keydown", function(event) {
  if (event.keyCode === 46 ) {
    $actions.DatePickerOnSelect_DeleteEnd();
  }
  event.preventDefault();
});
```

<br>

&nbsp;&nbsp;&nbsp;&nbsp; 1. I selected the Screen that contains de the Date
Pickers, **selected the OnReady option on its event property** to create the
*OnReady* action;

<br>
<div class="center-img">
  <img src="/images/os_datepicker-8.png"
  alt="Fig. 1. Setting OnReady event for the VacationCreationWidgets screen">
  <figcaption class="figcaption">
    Fig. 1. Setting OnReady event for the VacationCreationWidgets screen
  </figcaption>
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 2. On the flow of the *OnReady* action, **I added a
JavaScript widget**. I opened it, created as many input parameters as Date
Pickers on the screen — in my case, I created 2 and named them *StartContainerId*
and *EndContainerId*;

<br>
<div class="center-img">
  <img class="img-large" src="/images/os_datepicker-9-1.png"
  alt="Fig. 2.1. Adding a JS widget and the corresponding input parameters to
  the OnReady action">
  <figcaption class="figcaption">
    Fig. 2.1. Adding a JS widget and the corresponding input parameters to the
    OnReady action
  </figcaption>
</div>
<br>

I opened the JavaScript widget and added the snippet below (which is already
posted above);

<br>
<div class="center-img">
  <img class="img-large" src="/images/os_datepicker-9-2.png"
  alt="Fig 2.2. Adding the JS code to the JS widget">
  <figcaption class="figcaption">
    Fig 2.2. Adding the JS code to the JS widget
  </figcaption>
</div>
<br>

The JS input parameters should be **assigned to the id of the container that
surrounds each Date Picker** and corresponding Input widgets — check Fig. 2.1.
bottom right to see the containers being assigned to the JS input parameters.
We need to add a name to the containers to be able to assign them to the input
parameters.

<br>
<div class="center-img">
  <img src="/images/os_datepicker-9-3.png"
  alt="Fig. 2.3. Setting the name of the container to be able to assign it to
  the JS widget’s input parameters">
  <figcaption class="figcaption">
    Fig. 2.3. Setting the name of the container to be able to assign it to
    the JS widget’s input parameters
  </figcaption>
</div>
<br>

&nbsp;&nbsp;&nbsp;&nbsp; 3. The **delete actions** are pretty simple. I just
added an assign to clear the contents of each corresponding variable
*PickedBookingStartDate* and *PickedBookingEndDate*.

<br>
<div class="center-img">
  <img src="/images/os_datepicker-10.png"
  alt="Fig. 3. Setting up the delete actions">
  <figcaption class="figcaption">
    Fig. 3. Setting up the delete actions
  </figcaption>
</div>
<br>

That’s it!

<br>

If you have questions about any of the steps detailed above as well as anything
from [Part 1](https://twikah.github.io/work/2021/01/19/outsystems-datepicker-pt1.html)
of the guide or if you have suggestions to improve the
implementation of the Date Pickers, please reach out!
