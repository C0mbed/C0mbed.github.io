---
layout: post
title:      "Best Way to Fully Learn is To Jump Right In"
date:       2020-08-19 12:56:56 +0000
permalink:  best_way_to_fully_learn_is_to_jump_right_in
---


In many ways I found this project to be easier than the CLI project.  Writing ruby felt substantially more natural and creating the actual usable structure of my app was a reasonably smooth process.  While I didn't fully utlilize the planning process that we learned during the CLI Project, I did sketch out the direction I wanted to take before I started.  Unlike the first time, I didn't have to restart.  

Some initial areas of struggle were correctly using ```erb``` and ```sessions``` + shotgun.  In any case, I feel that upon completion I know have a thorough understanding of these concepts and won't run into the same issues again!  

## ERB

It wasn't intuitive to me to weave ruby using erb throughout my html files.  At first I struggled with structure and wanted to do all my ruby in the controller.  While, I could accomplish most of what I needed to in this fashion, I was unable to manipulate the html, and had looked at other more complicated options before deciding to learn how to correctly use erb.  

I was attempting to manipulate my ```nav bar``` to display the ```new car```, ```account``` and ```logout, [username]``` ```html``` elements ONLY IF the user was correctly logged in.  Since I was using ```bootstrap``` and ```jquery``` to help with the visuals, I thought I would use ```jquery``` and ```js``` to manipulate the ```DOM``` using the following: 

```
$(".nav-item").click(function(){
  $("a").hide();
});
```

Turned out this was a totally unnecessary step, and required a lot of complex code that I wasn't 100% familiar with (not to mention we aren't really working with ```js``` in this project!).  All I needed to do was use ```erb``` and a simple conditional to display the ```dom``` elements if the user was logged in:

```
<% if logged_in?%>
  <li><a href='/'>nav-item</a><li>
	<li><a href='/'>nav-item</a><li>
<%end%>
```

Four simple lines was all it took to accomplish what would have been a significantly more complex solution.  While finding this solution, I also learned why some ```erb``` is written ```<%=``` vs ```<%```.   The former displays the code (or product of the code) on screen, while the latter does not.  

## SESSIONS

Another area that I spent a considerable amount of time on were sessions.  After securing my sessions using ```sysrandom``` per the ```Sinatra Documentation``` I was unable to maintain an active session.  Turned out that ```shotgun``` continually refreshes, and if you are using a randomly generated key, you constantly lose the session.  

The solution was to randomly generate a 64-bit key using ```sysrandom``` and ```SecureRandom.hex(64)``` and placing it in an ```ENV``` variable called ```SESSION SECRET```.  

All in all, I thought this was a fun project.  Instead of a command line, we were able to significantly affect the visuals, and the code came alive on screen.  While I may not have fully understood erb and sessions when I began, I believe I finished with a complete understanding of both concepts and spent considerable time online researching.  


