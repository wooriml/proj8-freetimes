CIS 399se Project 8: Free times
Objectives
This is a continuation of project 7, and a milestone on the way to project 9 which will be the full meeting scheduling application. It introduces some algorithmic complexity in the web app. A key issue is good modularity so that the complex calculation can be developed and tested separately from the overall application.
Calculate available times by subtracting busy times from the proposed date and time ranges.
Thoroughly test the available time calculation separate from the overall applicaton.
Free Times
In the prior project you retrieved and displayed a set of appointments between a begin and end date, between a start and end time each day in that date range. Potential times for a meeting are the times within those ranges excluding the appointments.
For example, suppose we wanted to schedule a meeting between 9am and noon, Monday and Tuesday, but we found blocking appointments 10-11am on Monday, 8:30-9:30 on Tuesday, and 11-12:30 on Tuesday.

The available times for meeting would then be 9-10 Monday, 11-12 Monday, and 9:30-11 on Tuesday.

Project requirements
All requirements for Project 7 remain requirements for Project 8: You will display busy times that lie within or partially overlap the date and time ranges specified by the user, drawing those busy times from selected Google calendars.
In addition, you will calculate and display the free (non-blocked) time periods within the range. You may do this one of two ways:
Preferred: Display blocked and available times in a single list. For example, for the example illustrated above, for Monday you would list an available block from 9-10, class from 10-11, and another free block from 11-12. For Tuesday you would list class from 8:30-9:30, an available block from 9:30-11:00, and class from 11:00 to 12:30.
Also acceptable: You may display first the busy times, and then the available times in a separate list.
The user may determine that some of displayed events should not block his or her time. Permit the user to make a different selection of calendars after viewing the busy and available times.
The available time calculation should be a Python module in a separate source file. It must be accompanied by a thorough suite of nose tests.
Getting started
Your starter code for project 8 is your repository from project 7.
In the resources section of our Piazza site, under 'Libraries and Repos', you can find a module 'agenda.py' that performs a free time calculation similar to the one you need for this project. However, it does not use the arrow module, and the Appt and Agenda classes it defines are not suitable for display with Jinja2 because they lack conversions to JSON. You may find it a useful starting point, or at least a useful example. (For my implementation this summer, I started with this code, modified it to use Arrow for calculations, and added methods for converting to and from JSON.)
Above and beyond
Extra credit is available only if the project is turned in on time (by Friday at 5) and earns at least 80% credit for the requirements above. If you do that and want to do more, here are some refinements:
Time slivers
The requirements divide the day into free times and busy times. In our design discussions, we discussed a third category: Periods of time that are available but too short for a meeting. It would be nice if the user could specify a meeting duration, and if available times of less than that duration were suppressed from the display or displayed differently from potential meeting times. I will award up to 5 points extra credit for this feature.
Your feature
Got a cool idea to make the application more useful? Propose it to me by noon Thursday. If you convince me that it's a good idea, I will respond with the amount of extra credit I am willing to award for it.









# proj6-Gcal
Snarf appointment data from a selection of a user's Google calendars 

## What is here

I've provided code for the authorization (oauth2) protocol for Google
calendars.  There is also a picker for a date range. 

## What you'll add

You'll need to read the Google developer documentation to learn how to
obtain information from the Google Calendar service.

Your application should allow the user to choose calendars (a single
user may have several Google calendars, one of which is the 'primary'
calendar) and list 'blocking'  (non-transparent)
appointments between a start date and an end date
for some subset of them.

## Hints

You'll need a 'client secret' file of your own.  It should *not* be
under GIT control.  This is kind of a
developer key, which you need to obtain from Google.  See
https://auth0.com/docs/connections/social/google and
https://developers.google.com/identity/protocols/OAuth2 .
The applicable scenario for us is 'Web server applications'  (since
we're doing this in Flask).  

Your client secret will have to be registered for the URLs used for 
the oauth2 'callback' in the authorization protocol.  This URL includes
the port on which your application is running, so you you will need to 
use the same port each time you run your application. You can register 
the same key for multiple URLs, so for example I have registered mine
for localhost:5000/oauth2callback, localhost:8000/oauth2callback, 
roethke.d.cs.uoregon.edu:5000/oauth2callback, and 
roethke.d.cs.uoregon.edu:8000/oauth2callback. (Roethke is my raspberry Pi
at school.)  When we test your code, our grader and I will use our own 
admin_secrets.py and google credentials files, but we will use your 
client_secrets.py file.  As in the last project, your client_secrets.py
file should include a reference to your repository and to your name, 
so that our friendly (but clumsy) robots can use it to install your code. 

I have noticed that getting the list of calendars from Google is very very 
slow when running on my laptop at home, and snappier when accessing through
roethke.  I suspect that is because roethke.d.cs.uoregon.edu is is 
a routable IP address, while "localhost" on my home network requires some
behind-the-curtains magic from my home router.  I don't know that for sure. 

Whether or not you already have a Google calendar, it's a good idea to
create one or two 'test' calendars with a known set of appointments
for testing.



