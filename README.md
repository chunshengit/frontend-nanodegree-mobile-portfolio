Critical Rendering Path Optimization steps:
1. Image Optimization:
   views/images/Pizzeria.jpg file size reduced from 2.3MB to 29.kb with dimension scaled from 2048*1536 to 100*75,
   imag/profilepic file size reduced with dimension scaled from 100*70 to 70*70.

2. Rendering Blocking CSS Optimization:
   a. <link href="print.css"    rel="stylesheet" media="print"> is applied meida query to off the RCP.
   b. Inline minified css/style.css.
   c. Remove webfont stylesheet.

3. Remove Render-Blocking Javascripts:
   a. Make Javascript Asynchonous.
      <script async src="http://www.google-analytics.com/analytics.js"></script>
4. Inline Javascript.
    a. Inline <script src="js/performatters.js"></script> to reduce download size;
5. Further optimization can be done at the webserver side by applying HTTP cache.

The PageSpeed Insights improves from 28 to 96 for Mobile. Desktop at 97/100