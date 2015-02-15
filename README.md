# (Your) Steel-capped Toe

A little something (async state machine) to help out and signal when a webpage has indeed completed loading (and PARSING!) completely.

> "How do you start this thing?"
>
> "Oh, that's easy! We go around the back and prod it with our steel-capped toe. But in a *scientific way*, mind you!"
>
> (Paraphrased after Terry Pratchett: Ponder Stibbons explaining how to boot Hex, the magical computer in Unseen University.)


## Wat?

When you load a page, full of CSS and JavaScript, most problably stored in separate files (hence resulting in additional HTTP requests following the initial one), the browsers give you one event or another to signal that the JavaScript files and such have *loaded*.

What they do *not* do, however, is tell you when your hefty JavaScript files have actually *parsed* completely.

The difference between these two states of (browser) mind are subtle but *significant* as you will only be able to access the JavaScript functions and such, which you placed in those *external files*, after *both* the *load* **and** *parse* phases have completed. On all hardware, particularly when said hardware is already pretty loaded and thus a tad slower on the uptake right this instant, the latter *parse phase* takes non-negligable time. 

This becomes a problem when your 'boot code' is hooked into the browser's *load event*: that event can fire *too early* for your boot code to be able to actually access all the goodness ytou've been loading through external JavaScript files, causing very hard to diagnose 'random load/init errors', some of which will be very sneaky as they may only manifest themselves *indirectly* by failing to execute another piece of code much later during the period of time this web page is used by the user.

Hence it is paramount for (semi-)large JavbaScript-based web pages/applications to ensure that their boot/init process is guaranteed dependable and only running once all the dependencies have loaded *and parsed*.

That's what this little component is designed to help out with...
