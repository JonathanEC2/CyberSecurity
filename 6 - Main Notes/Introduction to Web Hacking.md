# Introduction to Web Hacking
## Exploring the Website

As a pen tester, your role when reviewing a website or web application is to discover features that could potentially be vulnerable and attempt to exploit them to assess whether or not they are. These features generally involve some interactivity with the user. 

Explore the website and note down the individual pages/areas/features with a summary for each one.

## Viewing the Page Source

The page source is the human-readable code returned to our browser/client from the web server each time we make a request.

- Always check for comments
- Explore all directories
- Check for clues of what web framework is being used. Knowing the framework and version can be a powerful find as there may be public vulnerabilities in the framework

## Developer Tools - Inspector

The page source doesn't always represent what's shown on a webpage. ; this is because CSS, JavaScript and user interaction can change the content and style of the page, which means we need a way to view what's been displayed in the browser window at this exact time. Element inspector assists us with this by providing us with a live representation of what is currently on the website.

## Developer Tools - Debugger

Called sources in Google Chrome

 Breakpoints are points in the code that we can force the browser to stop processing the JavaScript and pause the current execution. If you click the line number that contains the code, it creates a breakpoint.

## Developer Tools - Network

The network tab on the developer tools can be used to keep track of every external request a webpage makes. If you click on the Network tab and then refresh the page, you'll see all the files the page is requesting. 

AJAX is a method for sending and receiving network data in a web application background without interfering by changing the current web page.