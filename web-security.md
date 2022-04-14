# Web Security

## SQL Injection

## Cross-Site-Scripting (XSS)

-   A form of injection in the shape of malicious scripts

**Same Origin Policy** - Policy that stops one website from reading & writing to another

-   Protocol
-   Host
-   Port

**Protocol** - http or https?

**Host** - dankrzeminski.com or dankrz32.com

Javascript can steal csrf tokens and cookies

Having access on another website in another users context can be really problematic

Can we actually inject js into another webiste? Yes that is what xss is...

Take for example a user login...

USER lOGIN: danslogin123

That is the standard use case, but now take an instance where we are not preventing against xss and a hacker is on the site...

USER lOGIN: <script> Very Malicious Javascript! </script>

No matter what the user puts in the input, it will get rendered as html.

In the standard use case this is perfectly fine, but in the hacker's case we have malicious javacsript being entered into our server..

#### Reflected XSS

-   Input is reflected back in the response and gets executed as a script block

#### Stored XSS

-   Same as reflected XSS but the input is persisted and interacts with the database and then returns a response to the hacker.
-   Think of a youtube comment section, anyone who sees the comment gets infected by the script

#### DOM XSS

-   Entirely in the client side

-   User input lands in the inner html propery, so a string lands in the dom which can execute some javascript

-   svg onload="bad xss"

#### Mutation XSS

-   User input mutated by the browser before inputting DOM

-   Leads to cross site scripting

#### Hard problem

Preventing XSS is not easy

Blocking script tags is not enough to prevent xss

There are also event handlers which can execute javascript

Blocking tags is simply not a good solution...

-   Gmail and other mail services use html tags to send useful data
-   Html editors
-   MD editors

What then?

There are libraries you can use to sanitize your javascript and HTML

-   DOMPurify Library
