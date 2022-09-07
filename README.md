# Fullstack Open - part 0
Part 0 of the fullstack open online course https://fullstackopen.com/en/part0

## Exercise 0.1: HTML
**Task:**
Review the basics of HTML by reading this tutorial from Mozilla: [HTML tutorial](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics).

*This exercise is not submitted to GitHub, it's enough to just read the tutorial*

## Exercise 0.2: CSS
**Task:**
Review the basics of CSS by reading this tutorial from Mozilla: [CSS tutorial](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics).

*This exercise is not submitted to GitHub, it's enough to just read the tutorial*

## Exercise 0.3: HTML forms
**Task:**
Learn about the basics of HTML forms by reading Mozilla's tutorial [Your first form](https://developer.mozilla.org/en-US/docs/Learn/Forms/Your_first_form).

*This exercise is not submitted to GitHub, it's enough to just read the tutorial*

## Exercise 0.4: New note
**Task:**
In chapter [Loading a page containing JavaScript](https://fullstackopen.com/en/part0/fundamentals_of_web_apps#loading-a-page-containing-java-script-review) - review the chain of events caused by opening the page https://studies.cs.helsinki.fi/exampleapp/notes is depicted as a sequence diagram

The diagram was made using https://www.websequencediagrams.com/ service as follows:
```
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/notes
server-->browser: HTML-code
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.css
server-->browser: main.css
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.js
server-->browser: main.js

note over browser:
browser starts executing js-code
that requests JSON data from server
end note

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/data.json
server-->browser: [{ content: "HTML is easy", date: "2019-05-23" }, ...]

note over browser:
browser executes the event handler
that renders notes to display
end note
```

Create a similar diagram depicting the situation where the user creates a new note on page https://studies.cs.helsinki.fi/exampleapp/notes when writing something into the text field and clicking the submit button.

If necessary, show operations on the browser or on the server as comments on the diagram.

The diagram does not have to be a sequence diagram. Any sensible way of presenting the events is fine.

All necessary information for doing this, and the next two exercises, can be found from the text of [this part](https://fullstackopen.com/en/part0/fundamentals_of_web_apps#forms-and-http-post). The idea of these exercises is to read the text through once more, and to think through what is going on there. Reading the application [code](https://github.com/mluukkai/example_app) is not necessary, but it is of course possible.

**Solution:**
```
note right of browser:
assuming the page is loaded as shown in the task description
end note

note over browser:
user fills note text into the input field and clicks the submit button
end note

browser->server: HTTP POST https://studies.cs.helsinki.fi/exampleapp/new_note

note right of server:
POST request payload contains the note text from the input field
end note

note over server:
server reads and processes the note from the POST request payload
end note

server-->browser: HTTP 302

note right of browser:
browser reloads the page; 
the page is loaded as in the sequence diagram in the task 
and contains the new note
end note

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/notes
server-->browser: HTML-code
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.css
server-->browser: main.css
browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/main.js
server-->browser: main.js

note over browser:
browser starts executing js-code
that requests JSON data from server
end note

browser->server: HTTP GET https://studies.cs.helsinki.fi/exampleapp/data.json
server-->browser: [{ content: "HTML is easy", date: "2019-05-23" }, ...]

note over browser:
browser executes the event handler
that renders notes to display
end note
```

Visualized in Exercise-0-4.png

## Exercise 0.5: Single page app
**Task:**
Create a diagram depicting the situation where the user goes to the [single page app](https://fullstackopen.com/en/part0/fundamentals_of_web_apps#single-page-app) version of the notes app at https://studies.cs.helsinki.fi/exampleapp/spa.

**Solution:**
The page is loaded the same way as in the case above. Browser fetches HTML, then it goes through it and loads css, js and other files as defined.
The difference is in the content of the .js files content that takes over some of the responsibilities that are on the server side in traditional web applications.

## Exercise 0.6: New note
**Task:**
Create a diagram depicting the situation where the user creates a new note using the single page version of the app.

**Solution:**
```
note right of browser:
assuming the page is loaded
end note

note over browser:
user fills note text into the input field and clicks the submit button
end note

browser->server: HTTP POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa

note right of server:
POST request payload contains the note text from the input field
end note

note over server:
server reads and processes the note from the POST request payload
end note

server-->browser: 201 {"message":"note created"}

note over browser:
JS adds the new note to the least using DOM API / redraws the notes; no page reload is needed
end note
```