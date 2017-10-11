
<!-- .slide: data-background-image="./assets/md/assets/northfield1.png" data-background-size="auto 100%" -->


---

### Hacking Your Productivity
##### with
### Browser Userscripts
Jordan Neufeld

Note:
Hello, and welcome to **Hacking your Productivity with Browser Userscripts**

---

### Who I Am
<img width="240" src="./assets/md/assets/jordan-face.jpeg"/>

- Computer guy
- Musician

Note:
My name is Jordan Neufeld, and I work on the operations team at Northfield IT as a technical support consultant. I live in Winnipeg with my wife Claire, and I have no pets. In my spare time I make javascript do things on the internet, and somtimes I play the piano.

---

### The Agenda

- What are userscripts?  <!-- .element: class="fragment" -->
- What can they do?  <!-- .element: class="fragment" -->
- How to be awesome  <!-- .element: class="fragment" -->

Note:
In the Operations world we do a lot of repetitive work. I don't like doing repetitive work, so I like to automate stuff where I can. In this presentation, I hope to show you how you can leverage browser userscripts to automate pieces of your day to day workflow in your browser.

**ADVANCE**

We'll go over what userscripts are

**ADVANCE**

what they can do for you

**ADVANCE**

and how we've applied them at my workplace to achieve automation awesomeness.

---

### Userscripts: a different kind of automation

<img width="75%" src="./assets/md/assets/roll-safe-automation.jpg"/>

Note:
 On the Operations team where I work, we are responsible for the care and feeding of over 120 virtual machine hosts, 2000 plus virtual machines, dozens of microservices, legacy applications, and internal tools. We also handle thousands of technical support issues every year from our Client and their various vendors and partners. 

It's no surprise that we rely heavily on automation in order to perform  daily tasks. We've leveraged infrastructure-based automation using tools like Chef for bootstrapping new servers, bash scripts for health checks and automatic remediation, and even chatbot-based automation for scaling applications up and down as demand increases or decreases.

But today we're not talking about that traditional kind of infrastructure automation. Today we're going to explore a different kind of automation that is unlike scripts or apps that connect API's together. This kind of automation exists only in a single user's browser.

---

### Enter Userscripts

- We are NOT writing a browser extension  <!-- .element: class="fragment" -->
- We ARE extending functionality of webapps with a userscript browser extension  <!-- .element: class="fragment" -->

Note:
This new kind of automation that I'm referring to involves Userscripts. 

How many of you know what userscripts are, or have maybe used them before? 
Great, then you get to learn something new!


Userscripts are browser addons written in Javascript that allow you to modify any webpage as it is loaded. 

This means that we can change ANY webapp at runtime, and use this power to solve real problems in our workflow. 

**ADVANCE 1**

It's important to note that we are NOT writing a browser extension. These are often more complicated than necessary in order to solve simple problems.

**ADVANCE 2**

You can think of userscripts as extending functionality of existing websites with the help of a userscript browser extension. 

A userscript browser addon is first installed in a browser, and custom userscripts, written in javascript, are hosted by this browser extension, and are injected into websites that you visit.

This means that you can add that feature you've been longing for in in your favourite webiste, in order to solve a specific problem you have with it.

Put simply, userscripts allow you to inject your own custom javascript on top of any existing webpage at runtime.

---

### I'm getting bored, when does this get awesome?

- Very soon  <!-- .element: class="fragment" -->

Note:
If you've never seen userscripts in action, let me take this opportunity to show you the kinds of things that they can do. As I noted previously, you can use Userscripts to modify ANY website as it is loaded (especially sites that you didn't write and don't control). 

**ADVANCE**

This means you can do things like modifying the text, adding buttons, and even swapping out images.

---

#### Video Slide Disabled
#### [ GitPitch Offline ]

Note:

You'll notice that this cnn.com page looks rather normal, with the usual sad news, and sad images - but what if it didn't have to be so sad?

Let's install a tampermonkey script called cat news network.

To install it, i simply click on the link from github

Now that it's installed I just have to refresh the page.

You'll notice that I've injected a button in the top right-hand corner here that reads "This is too sad." When this button is clicked, I'm using the script replaces all of the images on this page with images from thecatapi.com, which is of course, everyone's favourite site for random cat images.

How does this help us deliver and run better software? You might think that it looks like a waste of time. 

Well, I for one believe smiling at work once and a while is NOT a waste of time, but that's just me

Of course, you can do much more with userscripts than just swapping out silly images on web pages - things that actually solve problems, and not just problems of boredom.

---

### I can haz the power?


<img width="400" src="./assets/md/assets/tampermonkey-logo.png">

<img width="400" src="./assets/md/assets/greasemonkey-logo.png">

#### Userscripts are just client-side javascript

Note:
Userscripts are easy to write. After all, they are just client-side javascript.

They run inside your browser via a browser extension. Because they only run inside your browser, no website or application code is ever modified on the server side. All userscripts live in a userscript library that is local to a user's computer.
Because userscripts are unique to every client visiting a webpage, they offer a unique experience to the user that allows them to personalize any website to their liking. 

In order to use userscripts, you need a userscript browser extension.

The most popular browser extensions for running userscripts are:
Tampermonkey, whose browser extension is available for Chrome, Firefox, Safari, Microsoft Edge, and more.

As well as Greasemonkey, which was one of the original userscript extensions, but is only available for Firefox.

For the remainder of this presentation, my examples will solely use the Tampermonkey extension, but they should also work on other userscript platforms.

---

### The Tampermonkey Library

<img width="800" src="./assets/md/assets/tampermonkey-homepage.png">

Note:
This is the tampermonkey script library interface, where all of my installed userscripts will live. Scripts that live in this library only live on my machine, and only affect webpages that I load. 

To install a script into your local script library, you have two options.

---

### Installing a script

<img width="800" src="./assets/md/assets/tampermonkey-script-installation-prompt.png">

Note:
Option 1 is to find an existing userscript online, and click on the URL to it. Userscripts are javascript, but have a special extension of `.user.js`. When you click on a URL that ends in `.user.js`, Tampermonkey will attempt to install the userscript for you, like you see here.

---

<img height="480" src="./assets/md/assets/stop-installing-random-scripts.jpg"/>

Note:
Of course, installing random scripts from the internet is probably not a good idea. Userscripts written with malicious intent can have real security issues that you should be aware of, like stealing your cookies, or passwords, etc. If you choose to install a script that you found online, you must read it first and understand what it is doing. Please exercise extreme caution when experimenting with userscripts that you did not write.


---

### The Tampermonkey Editor

<img width="800" src="./assets/md/assets/tampermonkey-editor-interface.png">

Note:
Option 2 for installing userscripts is writing one yourself (yay!). This is the reason why we're here today, to explore writing our own userscripts that will help us be more productive.

The Tampermonkey extension comes bundled with a built-in text editor interface where you can write your javascript code directly in the browser. You even get free syntax highlighting, and auto-indentation included.

---

### Basic Anatomy

```
// ==UserScript==
// @name         Cat News Network
// @version      0.1
// @description  Replaces images on CNN with images from www.thecatapi.com
// @author       Jordan Neufeld <jordan@neufeldtech.com>
// @match        http://www.cnn.com/*
// @require      https://code.jquery.com/jquery-3.2.1.min.js
// @updateURL    https://github.com/neufeldtech/userscripts/raw/master/cat-news-network.user.js
// ==/UserScript==


function doit() {
    var images = document.querySelectorAll('img');
    for (var image of images) {
        image.src = `https://thecatapi.com/api/images/get?format=src&type=jpg&_=${Math.random()}`;
    }
}
$(document).ready(function () {
    $('body').prepend('<button id="kittykat" style="position:fixed; top:50px; right:0px; z-index:10000000">This is too sad</button>');
    $('#kittykat').click(function () {
        doit();
    });
});
```
<span class="code-presenting-annotation fragment current-only" data-code-focus="1-9"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="2-5"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="6"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="7"></span>
<span class="code-presenting-annotation fragment current-only" data-code-focus="8"></span>

Note:
Let's take a look at what the source code looks like for the userscript that you just saw, the one that swaps out all website images with cat images on the website cnn.com.

**ADVANCE**

At the top of the script, we see some special comments, known as the userscript header.

**ADVANCE**

Name, version, description, and author are all pretty self-explanatory. They document the name of the script, the current version installed, a short description of what the script does, as well as the script's author.

**ADVANCE**

The @match directive tells Tampermonkey what pages that it should attempt to run the script on. Because userscripts are 100% client-side, they need to know what web pages to be injected into by the Tampermonkey browser extension that is managing them.

In my example, I've included a wildcard in my directive, because I want it to run on any page under the domain www.cnn.com.

**ADVANCE**

The @require directive is one that you'll make use of readily when writing userscripts. It is useful for making additional libraries available to your userscript code, such as jquery.

A lot of times websites already have jquery present, so you can often use that, but if they don't have it, you can pull jquery in with a `@require` statement.


**ADVANCE**

The UpdateURL directive is not required, but is helpful if you are sharing scripts with others. This directive allows tampermonkey to update the installed script automatically by checking the listed URL for a newer version than is currently installed.

When you have this configured, the tampermonkey extension will check for script updates on your behalf, and automatically update all clients with the latest version of your script.

---

### Pt 1

```
function doit() {
    var images = document.querySelectorAll('img');
    
    for (var image of images) {
        image.src = "https://thecatapi.com/api/images/get?format=src&type=jpg";
    }
}
```

Note:
Let's take a look at the actual code of this CNN.com userscript.
At the top, I have a function called `doit()`. This function is the main logic of the script. 

In the first line, I use document.querySelectorAll to select all of the image tags on the page and store it in an array.

In the second line, I loop through all of the elements in the array, and replace the image source attribute with an api call to thecatapi.com. 

---

### Pt 2

```
$(document).ready(function () {
    $('body').prepend('<button id="kittykat" style="position:fixed; top:50px; right:0px; z-index:10000000">This is too sad</button>');
    
    $('#kittykat').click(function () {
        doit();
    });
});
```

Note:
In the second half of the script is where I execute the code to actually make the image swaps.

The code is enclosed in a document.ready jQuery wrapper that will wait until the page has loaded before attempting to manipulate the DOM.
Once the page has loaded and ready, 

I insert button to the top of the page body with jquery.  This button has some inline style set to position it at the top-right of the page.

After the button is injected, I use jQuery's .click function to attach an event handler to the button, so that when it is clicked, it will run my doit() function.

---

<img width="800" src="./assets/md/assets/cat-news-network2.gif"/>

Note:
And that's all there is to the script. 
Once the script is installed, my javascript gets injected into the page after it loads, and voila! we see our button on the page.

---

### Not just for memes

<img width="800" src="./assets/md/assets/spacecat.jpg"/>

Note:
You might be thinking that userscripts are great for having a laugh, or playing a joke on a co-worker... and you'd be right.

But in all seriousness, we've leveraged the power of userscripts at Northfield IT to fill in automation gaps and work more efficiently, and I'll show you how.

---

### Tech Support intake lifecycle:

- Email comes into shared mailbox  <!-- .element: class="fragment" -->
- Classify and Create Ticket  <!-- .element: class="fragment" -->
- Reply to user professionaly with a clean, formatted email  <!-- .element: class="fragment" -->

Note:
Part of my job is intaking technical support requests and triaging them. Let's take a look at a typical tech-support intake workflow:

**ADVANCE**

- Email comes into shared mailbox.

**ADVANCE**

- Classify and Create Ticket

**ADVANCE**

- Reply to user in a professional manner with a clean, formatted email response.

These steps might all be manual tasks that are prone to human error and inconsistencies, especially when all support staff like to format their emails differently.

If you're fortunate enough to have a ticketing system is automatically integrated with your email, great!  

However - what happens when your workflow isn't as streamlined - maybe you have a unique use-case, or maybe you don't even manage the ticketing system you use.

Your intake procedure might look like this:

---

### The report

> I'm receiving an HTTP 418 every time I try to login to the site. Please help!

Note:

Suppose we received an email into the shared mailbox from a client. It reads: "I'm receiving an HTTP 418 every time I try to login to the site. Please help!"

---

### Classify and create ticket

<img width="800" src="./assets/md/assets/jira-autoresponse-ticket.png"/>

Note:
We can clearely see that a ticket is needed, So, we go to our ticketing software, and create a ticket with the information from the email.

Now we need to reply to the email quickly and professionally to let the client know that we are beginning work on their issue immediately.

---

### The response

<img width="800" src="./assets/md/assets/jira-autoresponse-email-poor-example.png"/>

Note:

We've now prepared an email response to the user's request for assistance. 
It reads: "hai i got ur msg and i create tkt 4 u # http://jira.example.com/ops-1234. kthxbai". 

**PAUSE**

We're really busy, you know, so we want to save time in emails by leaving out vowels, so we have more time for solving problems. However, this kind of email response does not reassure our client that we're prepared to solve their issue.

This scenario is a disaster with customer relationship management. When people report issues, they want to feel valued and re-assured that  their report has been received and will be actioned.

---

### The response (MK II)

<img width="800" src="./assets/md/assets/jira-autoresponse-ticket-with-tampermonkey.png">


Note:

In order to assist with this, one of my colleagues wrote a userscript specific to our use-case to fix the last piece of this tech-support intake workflow. This userscript is responsible for automatically generating a rich-text email response with details from a Jira ticket. 

Let's try again, but this time, we'll make use of the userscript to help us generate a professional, consistent email response.

Notice how the page looks with our userscript installed. You can see that our userscript is running on the page by the red dot on the Tampermonkey chrome extension. 

You'll also notice that there is a new link on the page called **OPS RESPONSE DIALOG**. This link was injected by our userscript code, it is NOT part of Jira itself. This link will help us by generating our email response on our behalf.

---

### The response (MK II)

<img width="800" src="./assets/md/assets/jira-autoresponse-ticket-with-tampermonkey-copied-to-clipboard.png">

Note:
When we click the link, we're prompted with a dialog box that has a few options for responding to the user. In this case, it's urgent so we'll selected the default option, labeled "We'll start working on your issue right away".
When this dialog box popped up, it copied a rich-text email response to our clipboard, so we're now ready to respond to the email.

---

### The response (MK II)

<img width="800" src="./assets/md/assets/jira-autoresponse-email-awesome-example.png">

Note:
The final step is to paste the contents of our clipboard into an email response. The result is what you see here - a rich HTML-styled email that clearly communicates that we've received their request for help, we're aware of the priority and we are prepared to action it immediately. The user also gets a description of the issue as we've captured it, and a link where they can receive updates on their issue. 

By having all of the members of our tech-support team install and use this script, we ensure that we are able to keep a clear, consise, and timely communication feedback loop to users that report issues via email. 
This userscript created a one-click solution for us, that reduces toil, and saves time in the tech-support intake workflow.

---

### Monitoring pains and the incident lifecycle

- Not all applications are as awesome as you are

Note:
Let's switch gears now and talk about incidents. Not a day goes by in the operations world without incidents. Some incidents are small, and some are large. Some incidents are user impacting and some are not. All incidents need to be remediated, and should be tracked.

Operations is filled with a wealth of dashboards, graphs, and interfaces that all are supposed to assist in identifying incidents as they happen.

Even though these monitoring applications may be trusted as de-facto standards by many organizations, many of these apps still have shortcomings in user experience, modularity and plugins. 

These deficiencies in user experience often result in users like me having to take extra steps to accomplish simple tasks that should have been one-click solutions.

I don't know about you, but I get frustrated when I have to dive through sub-menus to find the "Acknowledge Alert" button, especially when everything is on fire during an incident.

Let's look at an example of this toil during the incident lifecycle.

---

<img width="640" src="./assets/md/assets/incident-lifecycle.png">

Note:
This is an example of an incident lifecycle. It outlines the major steps that operations teams go through when the dashboard goes red.

- The unhealthy state, the dashboard goes red. Something is wrong, action is needed
- Create ticket for tracking
  - Creating the actual ticket
  - Acknowledge alert
  - Notify team members
- Triage initial impact
- Communicate the impact of the incident and the current status, if the incident is user impacting.
- Investigating and Remediating the incident
- Dashboard goes green, incident is remediated.

Application stakeholders don't like red lights on the dashboard. They want the time-to-remediation loop to be as short as possible.

A bottleneck on any stage of the incident lifecycle introduces the potential for increased user impact time. Any stage that takes longer to complete, blocks the rest of the cycle from reaching remediation as fast as possible.

Let me take you through the steps of just the 'create ticket' phase of the incident lifecycle, to show you what I mean, when I said that not all monitoring applications have a friendly user experience.

---

### Nagios

<img width="800" src="./assets/md/assets/nagios-all-services-plain.png"/>

Note:

Of course, I'm talking about Nagios.

We use Nagios as one of our core systems for monitoring and alerting. Nagios is one of the industry-standards for infrastructure monitoring, but it's user experience leaves a lot to be desired.

When an alert in Nagios goes critical, an OPS engineer is responsible for creating an incident ticket for this alert. This meant tediously copying and pasting the information from the Nagios UI into a Jira ticket. 

---

### Creating the ticket

<img width="800" src="./assets/md/assets/nagios-jira-ticket.png"/>

Note:
Creating an incident ticket from a Nagios alert involves these steps:
- Open Nagios and Jira in browser
- Write ticket title, this means copy/pasting from nagios
- Write ticket description - This involves Copying and pasting 3 different pieces of information from the nagios UI to Jira. It means that you have to switch browser tabs 3 times, copying and pasting 3 different pieces of info in order to get all of the required details for the ticket.

---

### Communicating

<img width="640" src="./assets/md/assets/nagios-slack-note.png"/>

Note:

- After the ticket is finally created, you will need to provide the URL of the ticket to your team via Slack, so they know what's broken, and they can help fix it.

---

### Acknowledge Alert

<img width="800" src="./assets/md/assets/nagios-service-detail-plain-ack-problem.png"/>

Note:
You're not done yet... After your team has been notified, you'll still need to acknowledge the alert in nagios with a comment indicating ticket number for the Alert.

This involves drilling down into the specific alert screen and waiting for the lagging user interface to catch up. Remember, things might be on fire at this point... any time wasted by waiting for a slow user interface, is more time that users are impacted.

---

<img width="640" src="./assets/md/assets/incident-lifecycle-create-ticket-bottleneck.png"/>

Note:

 This flow I'm describing is time consuming, monotonous, and error-prone. This workflow was the cause of an unnecessary bottleneck in the incident lifecycle, and it directly affected time to remediation.
 
 Extra manual labor for creating incident tickets from alerts also introduces alert fatigue. If an operator is burdened by these extra steps, human nature says that they will likely want to perform this task less often.  When fewer incidents are documented, the business loses visibility, which can lead to blindness of repeated incidents, or what could be described as 'chronic problems'.

I was a victim of Alert fatigue due to this workflow. I was spending too much time creating incident tickets rather than fixing them, so I decided to look for a solution to un-block this bottleneck.

I needed a way to create incident tickets from Nagios in as few clicks as possible, with minimal to no copying and pasting.

---
### Eliminating toil

##### Goal: fast and pain-free incident ticket creation

- Write a script to tail Nagios logfile  <!-- .element: class="fragment" -->
- Add code to Nagios PHP frontend  <!-- .element: class="fragment" -->
- Write client-side userscript to inject button into the Nagios frontend  <!-- .element: class="fragment" -->

Note:
Let's explore some possibilities for solving this issue of alert fatigue:

**ADVANCE**

- Could write a script to poll nagios logfile and create jira tickets when it sees `CRITICAL`
  This approach would allow zero-touch ticket creation, which is great, but let's be honest, there would be way too many false positives and ticket-explosions if we didn't have some human filtering in place.

**ADVANCE**

- Could re-write some of the Nagios PHP frontend to include a button for creating tickets. This would be awesome to fix the Nagios UI to include a Jira ticket button. However, I'm not a PHP dev, and the development effort on this seemed daunting. Also, it's probably not a good idea to introduce code that might break your monitoring tools.
  

**ADVANCE**

- Could write a Userscript to inject a button into the page to create a Nagios ticket.
  
  This effort would have minimal development time, as I can write it in Javascript and not PHP.
  
  This approach is low-risk, because I'm only affecting the Nagios User interface in my browser. I don't put the whole application at risk, because my script is injecting javascript local to my machine.
  
---

### The Solution

<img width="800" src="./assets/md/assets/nagios-all-services-tampermonkey-zoomed.png">

- Creates Jira ticket
- Copies the created ticket URL to clipboard
- Acknowledges Nagios Alert
- Posts notification to Slack

Note:
I ended up choosing the third option.
I wrote a Userscript that would inject new functionality overtop of the existing Nagios User Interface to help un-block the 'create ticket' portion of the incident lifecycle.

You can see in the image above that there is a new jira logo button injected into the nagios DOM. This button is not native to nagios, but was injected by my userscript.

When I click this button, the Userscript's javascript code does 4 things for me:
- First, it makes a call to our Jira API to create a ticket based on the information that it scraped from the Nagios DOM. Including the Hostname, service name, and description fields. No more context switching!
- Copies the URL to the ticket that it created to my clipboard, for convenience, for when I need update it.
- Sends API call to Nagios to Acknowledge the Alert on my behalf, and it even includes the ticket number in the acknowledgement comment.
- And finally, it will POST to a Slack Webhook on my behalf, so that my colleagues are alerted in Slack that I just created an incident ticket for this alert.

---

### Achievement unlocked

<img width="640" src="./assets/md/assets/first-day-on-internet-kid.png"/>

Note:
Accomplishing these 4 actions with one click means that I had removed the pain points from the `Create ticket` step of the incident lifecycle.

 This userscript enabled us to reduce the 'create ticket' process from 7 manual steps, to one mouse click. 
 
 This effectively removed the bottleneck in our incident lifecycle, which means that we now are able to move faster during incidents, and reduce the overall time to remediation.

---

### Moar Advanced Awesomeness

- `GM_setValue()`, `GM_getValue()`
- `GM_setClipboard()`
- `GM_download()`
- `GM_xmlhttpRequest()`

Note:
You've now been introduced to the basics and seen what userscripts can do, so let's dig a little deeper into some userscript functions that made it possible to write these scripts.

The Tampermonkey and GreaseMonkey extensions each contain API methods that enhance the userscript writing experience.
Some of the built-in API methods offer functionality like getting/setting values in a key-value store, copying data to the clipboard, downloading files, and even making cross-domain HTTP calls that bypass cross-origin browser restrictions.

---

### Grants

```
// ==UserScript==
// @grant GM_setValue
// @grant GM_getValue
// @grant GM_setClipboard
// @grant GM_download
```

Note:
As you might imagine, a userscript that has access to make cross-domain calls, access your clipboard, and download files has the potential to be a security risk, especially if you have installed a userscript that you did not write.

This is where grants come in. 
The `@grant` directive is part of the Userscript header block, and these directives give permissions to use the built-in API methods that start with GM underscore.

If a script tries to invoke a GM_ method that has not been granted, an error will be thrown as the method will be undefined.

If you are installing a script that you did not write, you should inspect the userscript header to see what permissions the script is requesting.

---

### Same-Origin-Policy

<img width="800" src="./assets/md/assets/cors-error.png"/>

`xmlhttpRequest has been blocked because no Access-Control-Allow-Origin header is present on the requested resource` :(

Note:
Those of you that have written any client-side javascript before will recognize the error above. It says that our xmlhttpRequest has been blocked because no `Access-Control-Allow-Origin` header is present on the requested resource.
This error can happen when we attempt to make an HTTP request with javascript to a different domain than the one we are currently on. 

This is a security feature implemented by browsers to keep users safe, and is known as the **Same Origin Policy**. While keeping users safe is a good idea, the same origin policy often means that developers need to find work-arounds to make cross-domain calls in the browser.

---

### No More Cors
```
// ==UserScript==
// @grant GM_xmlhttpRequest
// @connect google.com
```

Note:
Fortunately for us, Tampermonkey has an API method that allows us to override the same-origin-policy, which means we can make cross-domain requests to any resource we want.
In order to take advantage of this new power, we need to add 2 more lines to our userscript header.
The `@connect` directive in the header, specifically grants our userscript permission to make cross-domain http requests to the listed domain. 

The `@grant` directive, which grants us the use of the special GM_xmlhttpRequest API method, which we can use to make these cross-domain calls that bypass the restrictions of the same-origin-policy.

---

<img width="480" src="./assets/md/assets/oprah-cookies.jpg"/>

 GM_xmlhttpRequest sends browser cookies cross-domain, so you probably don't need to build in auth into your HTTP calls.

Note:
The power behind `GM_xmlhttpRequest` is really exercised when you use it to make HTTP calls between web applications. This is because after you have granted the correct permissions to this API method, it automatically sends all the cookies that your browser would normally send to the requested domain.

For example, in my previous script where I was creating a jira ticket from the Nagios user interface, I never hard-coded any credentials into my userscript. 

When I made an HTTP request from the Nagios Interface using `GM_xmlhttpRequest`, my browser sent my Jira cookie with the request to the Jira server. As long as I had a valid Jira login session in my browser, my call to the Jira API succeeds.

---

### Demo

`github.com/neufeldtech/userscripts`


Note:

I have a few demos to show you now that will help me demonstrate some more things that userscripts can do. If you'd like to follow along and check out the code for these demo scripts, please visit github.com/neufeldtech/userscripts.

```
cd ~/dev/nt/atlassian-jira-software-7.5.0-standalone/
bin/start-jira.sh
```

### Github Color Picker
- Navigate to https://github.com/neufeldtech/userscripts/?demo1
- Install Tampermonkey
- Show installation of github colorpicker
- Show Usage of github colorpicker
- Stores the color choice in localstorage, and applies the stored color on page load

Takeaways:
- Menu integration
- Personalization

### Slack Jira ticket creator
- Originally wrote this for work, to try to reduce context-switching in a fast paced environment
- Demonstrating it in the Prairie Tech Slack room. If you're not there already, you should join at Slack.prdcdeliver.com!
- This script allows a user to create a jira ticket directly from a Slack message, without ever leaving Slack itself!

Takeaways:
- Reduce context switching
- Immediate feedback for clients
- Sometimes a UI is what you need rather than Bot Syntax


### Slack Automoji

- The final script I'm going to show you today is one that might get you in trouble. It's not very practical at this time, but I wrote it as a proof of concept to show that you can hook into the Slack APIs very easily from the slack Web interface.

This script connects to the Slack websocket API on your behalf, listens for incoming messages, and then will post a reaction of your choice to each and every message coming in.

Takeaways:
- Use existing boot token from the DOM (no auth!)
- Fancy things, like websockets

The great thing about using Tampermonkey for this, is that anyone can install it and have it work immediately because the script pulls your API token directly from the DOM. 

---

### Go forth and script!

Script ideas and examples
- <a target="_blank" href="https://greasyfork.org">greasyfork.org</a>
- <a target="_blank" href="https://openuserjs.org">openuserjs.org</a>

Docs
- <a target="_blank" href="https://tampermonkey.net">tampermonkey.net</a>

Note:
I hope that by now these examples that I've shown are giving you ideas of how you'd like to try to leverage userscripts to solve a problem that you have in your own workflow. 

If you're still looking for more ideas, there are several popular userscript repositories that you can browse for inspiration. greasyfork.org and openuserjs.org are good places to look.

If you're ready start writing your own userscripts then you should check out the official documentation at tampermonkey.net to familiarize yourself with the full API that's built into the Tampermonkey extension.

---

### Acknowledgement
Thanks to Mike Menzies, Tampermonkey enthusiast and DOM hacker

Note:
I want to take a moment to acknowledge one of my colleagues, Mike Menzies.  He's the guy who got me into userscripts, and some of the scripts you saw today are his creations. Thanks for letting me include your work today Mike!

---

### Questions

- 🐦 @jordanband 
- 📧 jordan@neufeldtech.com

---
<!-- .slide: data-background-image="./assets/md/assets/Sponsor_WhiteBackground.jpg" data-background-size="auto 90%" -->