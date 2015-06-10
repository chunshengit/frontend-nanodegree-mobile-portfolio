Project 4:

This project is hosted at: http://chunshengit.github.io/frontend-nanodegree-mobile-portfolio/
The submission of the project is main branch.

Part One: Critical Rendering Path Optimization steps

(All the files are relative to root directory)

1. Image Optimization to reduce the download bytes

   views/images/Pizzeria.jpg file size reduced from 2.3MB to 29.KB with dimension scaled from 2048*1536 to 100*75,
   imag/profilepic file size reduced with dimension scaled from 100*70 to 70*70.

2. Rendering Blocking CSS Optimization

   a. Media query is added to css/print.css to take it off the CRP.
   b. Inline minified css/style.css.
   c. Remove webfont stylesheet.

3. Remove Parsing-Blocking Javascripts

   a. Make Javascript Asynchonous.
      <script async src="http://www.google-analytics.com/analytics.js"></script>

4. Inline Javascript

    a. Inline <script src="js/performatters.js"></script> to reduce download size also.

5. Further optimization can be done at the webserver side by applying HTTP cache.

The PageSpeed Insights improves from 28/100 to 96/100 for Mobile. Desktop scores at 97/100

Part Two:Optimize Frames per Second in pizza.html

1. Timeline tracing indicates less than 60FPS performance due to FLS and the bottleneck is at the constant updatePositions(). Further scrunitize indicates
   200 pizzas are generated at the page load. For regular viewport, only a small amount of pizzas are really needed. So first optimization effort is
   to only generate enough pizzas fitting current viewport dimension. Second in the updatePositioins() function, every pizza style.left is calculated and
   updated when the browser window is scrolled. scrollTop remains the same for each scoll action. There is no need to calculate the phase value for each
   pizza in the loop as modulus operation only generates fixed number of values. The second optimization effort is precacluated the phase value and only
   update each pizza element phase in the loop to reduce the javascript run time overhead. After these two steps, performance improves and close to 60FPS
   but painting still takes quite some time. To give the browser some hints on the painting optimization, "transform" and "translateZ()" are added to the CSS. Now page runs at below 60FPS consistenly.

2. Slide the slider to choose recipe for pizzas and Time to resize pizzas at 170ms seconds. TimeLine trace indicates that  Forced Synchronous Layout
   caused by function determineDx(elem, size) at Line 426 which is repeated called by changePizzaSizes(size) at Line 454. Refactor changePizzaSize(size)
   to simplify the pizza size style change by following the instructor directions in the course. Time to resize pizza now at 1ms and below.