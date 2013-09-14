# Animating JavaScript

                 /\__
        .--.----'  - \
       /    )    \___/
      |  '------.___)
       `---------`
		@nicknisi

# What are we talking about?

We played FightCodeGame back in August at @NebraskaJS.

JavaScript-powered tanks battle it out on a canvas, all within your browser

	   __                             __
	 _[__]_===       (bang).....>===_[__]_
	(______)	                   (______)

		(Slightly Better Graphics)

> We'll play this today :-)

# What's powering this?

* canvas
	* <canvas width="960" height="640"></canvas>
* 2D context
	* objects, methods, and properties to draw and manipulate graphics on canvas
	* document.querySelector('canvas').getContext('2d');
* Server-side component
	* There's a hidden element on the page with the battle winner on page load

# Drawing on the canvas

```html
<!doctype html>
<html>
    <head></head>
	<body>
		<canvas id="canvas" width="960" height="640"></canvas>
		<script>
			(function () {
				var canvas = document.getElementById('canvas'),
					context = canvas.getContext('2d'),
					x = canvas.width / 2,
					y = canvas.height / 2,
					radius = 130;

				context.beginPath();
				context.arc(x, y, radius, 0, 2 * Math.PI, false);
				context.fillStyle = 'purple';
				context.fill();
				context.lineWidth = 5;
				context.strokeStyle = '#000000';
				context.stroke();

			})();
		</script>
	</body>
</html>
```

# Drawing an image to the canvas

* Simple, but we have to wait for the image to load

```html
<!-- beakly.html -->
<canvas id="canvas" width="450" height="600"></canvas>
<script>
    (function () {
        var canvas = document.getElementById('canvas'),
            context = canvas.getContext('2d'),
            image = document.createElement('img');
        image.onload = function () {
            context.drawImage(image, 0, 0);
        };

        image.src = 'images/beakly.png';
    })();
</script>
```

# Selecting part of an image to draw

* Sprites!

```javascript
context.drawImage(
    image, // the image to draw
    tileX, tileY, // coords on the image to start drawing from
    tileWidth, tileHeight, // rectangle from coords to capture
    x, y, // where on the canvas we want to place
    destWidth, destHeight // the size we want to draw on the canvas
);
```

Let's draw a single frame

```html
<!-- nick.html -->
<canvas id="canvas" width="450" height="600"></canvas>
<script>
    (function () {
        var canvas = document.getElementById('canvas'),
            context = canvas.getContext('2d'),
            image = document.createElement('img');
        image.onload = function () {
            context.drawImage(
                image, // superbrown.png
                64, 64, // coords inside image
                64, 64, // width, height of tile,
                0, 0, // coords of where to start painting
                450, 600 // width, height to paint on canvas
            );
        };

        image.src = 'images/superbrown.png';
    })();
</script>
```

# Animating!

* Draw image tile
* Erase image
* Draw another image tile
* Repeat!

# What we need is a loop!

       .( * .
    .*  .  ) .
   . . POOF . .
    '* . (  .) '
     ` ( . *

# Create an animation loop

> -setTimeout-
> -setInterval-

* Always runs, even when the tab is hidden/off-screen
    * Chrome throttles to 1fps
* updates the screen when it wants to, not when the screen is ready

# requestAnimationFrame

tell the browser to execute your callback before the next repaint

* Can occur up to 60x/second
* Supported everywhere & IE10+
    * some vendor prefixes
    * polyfill! https://gist.github.com/joelambert/1002116

```javascript
requestAnimationFrame(function step(hiResTimestamp) {
    if (someCriteria) {
        // call again, thus creating the loop
        requestAnimationFrame(step);
    }
    // perform rest of callback
});
```

# JavaScript Game Engines

* 2D
    * http://impactjs.com/
    * http://frozenjs.com/docs/
    * http://craftyjs.com/
    * http://gamequeryjs.com/

* 3D
    * http://threejs.org/

# Animations for FUN!

* enhance your blog/site
* show off some skills
* enhance with other technologies
    * Web Speech API
    * WebRTC

# Thank you
                 .-._
      )         {_}^ )'
     /`----------`/~`
    (_(--------(_(
