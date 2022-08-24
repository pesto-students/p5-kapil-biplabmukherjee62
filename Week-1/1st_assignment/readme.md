a.What is the main functionality of the browser?

Ans:- The browser  is an application software that allows users to find,
access, display, and view websites Below are some of the main functions
of web browsers

-   The main task is to collect information from the Internet and make
    it accessible to users.

-   A web browser can be used to visit any website. When we type a URL
    into a browser, the web server redirects us to that website.

-   Plugins are available on the web browser to run Java applets and
    flash content.

-   It simplifies Internet surfing because once we arrive at a website,
    we can quickly check the hyperlinks and access a wealth of
    information.

-   Internal cache is used by browsers and is saved so that the user can
    open the same webpage multiple times without losing any data.

-   A web browser can open multiple web pages at the same time.

-   Back, forward, reload, stop reload, home, and other options are
    available on these web browsers, making them simple and convenient
    to use.

Here is the diagram how browser send request to web server and receive
the response form server

![](vertopal_f37dce08d8744d939575cb66bb3d0e87/media/image1.png){width="5.275in"
height="2.5055555555555555in"}

b.High Level Components of a browser.

## The main components of the browser include:

1\. The user interface - including the address bar, back/forward
buttons, bookmarks directory, etc., that is what you see other than the
main window used to display the page you requested

2\. Browser engine - the interface used to query and operate the
rendering engine

3\. Rendering engine - used to display the requested content, for
example, if the requested content is html, it is responsible for parsing
html and css, and displaying the parsed results

4\. Network - used to complete network calls, such as http requests, it
has a platform-independent interface and can work on different platforms

5\. UI backend - used to draw basic components such as combo selection
boxes and dialog boxes, with a general interface that is not specific to
a certain platform, and the bottom layer uses the user interface of the
operating system

6\. JS interpreter - used to interpret and execute JS code

7\. Data storage - belongs to the persistence layer. The browser needs
to save various data similar to cookies in the hard disk. HTML5 defines
the web database technology, which is a lightweight and complete
client-side storage technology.

**C. Rendering engine and its use.**

Ans :- Rendering Engine: As the name suggests, this component is
responsible for rendering a specific web page requested by the user on
their screen. It interprets HTML and XML documents along with images
that are styled or formatted using CSS, and a final layout is generated,
which is displayed on the user interface.

**D. Parsers (HTML, CSS, etc)**

Ans:- A parser is a compiler or interpreter component that breaks data
into smaller elements for easy translation into another language. A
parser takes input in the form of a sequence of tokens, interactive
commands, or program instructions and breaks them up into parts that can
be used by other components in programming.

**E. Script Processors**

=\>Ans:- The script processor executes Javascript code to process an
event. The processor uses a pure Go implementation of ECMAScript 5.1 and
has no external dependencies. This can be useful in situations where one
of the other processors doesn't provide the functionality you need to
filter events.

The processor can be configured by embedding Javascript in your
configuration file or by pointing the processor at external file(s).

f\. Tree construction

=\> First, the browser combines the DOM and CSSOM into a \"render
tree,\" which captures all the visible DOM content on the page and all
the CSSOM style information for each node.

![](vertopal_f37dce08d8744d939575cb66bb3d0e87/media/image2.png){width="7.067361111111111in"
height="2.2319444444444443in"}

To construct the render tree, the browser roughly does the following:

1.  Starting at the root of the DOM tree, traverse each visible node.

    -   Some nodes are not visible (for example, script tags, meta tags,
        and so on), and are omitted since they are not reflected in the
        rendered output.

    -   Some nodes are hidden via CSS and are also omitted from the
        render tree; for example, the span node\-\--in the example
        above\-\--is missing from the render tree because we have an
        explicit rule that sets the \"display: none\" property on it.

2.  For each visible node, find the appropriate matching CSSOM rules and
    apply them.

3.  Emit visible nodes with content and their computed styles.

g.Order of script processing

=\> Since the JavaScript on your page executes based on certain factors,
let\'s consider where and how to add JavaScript to a web page. 

There are basically three locations into which we can attach JavaScript:

-   Directly into the head of the page

-   Directly into the body of the page

-   From an event handler/listener

It doesn\'t make any difference whether the JavaScript is [[within the
web
page]{.ul}](https://www.thoughtco.com/moving-javascript-out-of-the-web-page-2037542) itself
or in external files linked to the page. It also doesn\'t matter whether
the event handlers are hard-coded into the page or added by the
JavaScript itself (except that they can\'t be triggered before they are
added).

![](vertopal_f37dce08d8744d939575cb66bb3d0e87/media/image3.png){width="5.933333333333334in"
height="1.3916666666666666in"}

shows an interesting pattern. The first JavaScript file begins to
download and blocks any of the other files from downloading in the
meantime. Further, there is a delay between the time at
which *file1.js* is completely downloaded and the time at
which *file2.js* begins to download. That space is the time it takes for
the code contained in *file1.js* to fully execute. Each file must wait
until the previous one has been downloaded and executed before the next
download can begin. In the meantime, the user is met with a blank screen
as the files are being downloaded one at a time. This is the behaviour
of most major browsers today.

H. Layout and Painting

=\> The output of the layout process is a \"box model,\" which precisely
captures the exact position and size of each element within the
viewport: all of the relative measurements are converted to absolute
pixels on the screen.

Finally, now that we know which nodes are visible, and their computed
styles and geometry, we can pass this information to the final stage,
which converts each node in the render tree to actual pixels on the
screen. This step is often referred to as \"painting\" or
\"rasterizing.\"

This can take some time because the browser has to do quite a bit of
work. However, Chrome DevTools can provide some insight into all three
of the stages described above. Let\'s examine the layout stage for our
original \"hello world\" example:

![](vertopal_f37dce08d8744d939575cb66bb3d0e87/media/image4.png){width="6.692361111111111in"
height="1.875in"}

-   The \"Layout\" event captures the render tree construction,
    position, and size calculation in the Timeline.

-   When layout is complete, the browser issues \"Paint Setup\" and
    \"Paint\" events, which convert the render tree to pixels on the
    screen.

The time required to perform render tree construction, layout and paint
varies based on the size of the document, the applied styles, and the
device it is running on: the larger the document, the more work the
browser has; the more complicated the styles, the more time taken for
painting also (for example, a solid color is \"cheap\" to paint, while a
drop shadow is \"expensive\" to compute and render).

The page is finally visible in the viewport:

![](vertopal_f37dce08d8744d939575cb66bb3d0e87/media/image5.png){width="7.469444444444444in"
height="3.854861111111111in"}

Here\'s a quick recap of the browser\'s steps:

1.  Process HTML markup and build the DOM tree.

2.  Process CSS markup and build the CSSOM tree.

3.  Combine the DOM and CSSOM into a render tree.

4.  Run layout on the render tree to compute geometry of each node.

5.  Paint the individual nodes to the screen.
