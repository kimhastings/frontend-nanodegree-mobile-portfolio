# Website Performance Optimization portfolio project

To view the optimized portfolio online, click [here](https://kimhastings.github.io/mobile-portfolio/)

If you would like to view the portfolio locally on your computer:

* Click [here](https://github.com/kimhastings/mobile-portfolio) to open the repository where the code is stored
* Click on the green "Clone or download" button in the upper right corner of the page
* Click on "Download ZIP"
* Save the zip file on your computer and then unzip it
* Open the unzipped folder called "mobile-portfolio-master" and click on index.html to open the portfolio

## Optimizations Made

### Avoid Render Blocking CSS

Inlined styles.css in index.html

Used Webfont Loader to load Google fonts

### Optimize images

Optimized all images, but especially pizzeria.jpg which was huge

### Computational Efficiency

Deleted unnecessary function determineDx() from views/js/main.js

Pizza slider improved by eliminating layout thrashing

Before:

```
    for (var i = 0; i < document.querySelectorAll(".randomPizzaContainer").length; i++) {
      var dx = determineDx(document.querySelectorAll(".randomPizzaContainer")[i], size);
      var newwidth = (document.querySelectorAll(".randomPizzaContainer")[i].offsetWidth + dx) + 'px';
      document.querySelectorAll(".randomPizzaContainer")[i].style.width = newwidth;
```

After:

```
    // Get the pizza elements
    var divs = getDomNodeArray('.randomPizzaContainer');
  
    // Iterate through pizza elements on the page and change their widths
    divs.forEach(function(element) {
      element.style.width = newWidth + "%";
    }, this); 
```

Sliding background pizzas improved by eliminating layout thrashing

Before:

```
  var items = document.querySelectorAll('.mover');
  for (var i = 0; i < items.length; i++) {
    var phase = Math.sin((document.body.scrollTop / 1250) + (i % 5));
    items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
  }
```

After:

```
  // Get the background pizza elements
  var divs = getDomNodeArray('.mover');

  // Iterate through background pizza elements on the page and change their positions
  divs.forEach(function(element,index) {
    var phase = Math.sin((document.body.scrollTop / 1250) + (index % 5));
    element.style.left = element.basicLeft + 100 * phase + 'px';
  }, this); 
```

