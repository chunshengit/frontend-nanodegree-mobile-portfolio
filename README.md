Project 4:

Part One: Critical Rendering Path Optimization steps

(All the files are relative to root directory)

1. Image Optimization to reduce the download bytes
   views/images/Pizzeria.jpg file size reduced from 2.3MB to 29.KB with dimension scaled from 2048*1536 to 100*75,
   imag/profilepic file size reduced with dimension scaled from 100*70 to 70*70.

2. Rendering Blocking CSS Optimization
   a. Media query is added to css/print.css to take it off the CRP.
   b. Inline minified css/style.css.
   c. Remove webfont stylesheet.

3. Remove Parsing-Blocking Javascripts:
   a. Make Javascript Asynchonous.
      <script async src="http://www.google-analytics.com/analytics.js"></script>

4. Inline Javascript.
    a. Inline <script src="js/performatters.js"></script> to reduce download size also.

5. Further optimization can be done at the webserver side by applying HTTP cache.

The PageSpeed Insights improves from 28/100 to 96/100 for Mobile. Desktop scores at 97/100

Part Two:Optimize Frames per Second in pizza.html

1. Scroll the sidebar and background moving pizzas are not contributing anything new to the page and cause visual satuation.
   User Timing API frame data to console indicates average time to generate 10 frames at 24ms to 30ms which is just for generating all the random pizzas in the background. Timeline tracing indicates Forced Synchronous Layout caused by function updatePositions at line 507. Indeed document.body.scrollTop is accessed and causes re-layout. As we already have too too many pizzas on the pages, we are better off just remove this function from the Windows eventListener list.

2. Slide the slider to choose recipe for pizzas and Time to resize pizzas at 170ms seconds. TimeLine trace indicates that  Forced Synchronous Layout caused by function determineDx(elem, size) at Line 426 which is repeated called by changePizzaSizes(size) at Line 454.
Refactor changePizzaSize(size) to simplify the pizza size style change by following the instructor directions in the course. Time to resize pizza now at 1ms and below.