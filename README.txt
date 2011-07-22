This is a simple dragging library for JavaScript.

To make an object draggable with DOM-drag, you call Drag.init( ), and pass it a 
reference to the object you want to drag. The function also accepts a whole
slew of other parameters, but lets not get ahead of ourselves.

If you had this image in your HTML:

<img id="foo" src="foo.gif" />		

... then you could use the following code to make it draggable:

<script language="javascript">
	Drag.init(document.getElementById("foo"));
</script>


Note:
    * You have to absolutely or relatively position the element you want to be
      draggable.
    * You have to position the element inline with the STYLE attribute.
    * You have to call Drag.init( ) after the element is loaded - either after
      the element in the source, or in the .onload( ) handler.


You can make one DOM element a "handle" for another DOM element by passing both
elements to init():

<script language="javascript">
	var theHandle = document.getElementById("handle");
	var theRoot   = document.getElementById("root");
	Drag.init(theHandle, theRoot);
</script>


You can limit the area that you can drag the element to using additional params
to init():

<script language="javascript">
	var aThumb = document.getElementById("thumb");
	Drag.init(aThumb, null, 25, 25, 25, 250);
</script>

They go in the order: minX, maxX, minY, maxY. If for some reason you only need
to set a few of these, you can set the others to null to tell DOM-Drag that
motion in that direction should not be constrained.


You can get events from DOM-Drag:

...
var scroll = new ypSimpleScroll("scroller", 2, 2, 142, 100
...
var aThumb   = document.getElementById("thumb");
Drag.init(aThumb, null, 25, 25, 25, 250);

// the number of pixels the thumb can travel vertically (max - min)
var thumbTravel = 225;

// the ratio between scroller movement and thumbMovement
var ratio = aThumb.scrollH / thumbTravel;

aThumb.onDrag = function(x, y) {
	scroll.jumpTo(0, Math.round((y - 225) * ratio));
}
...


Finally, you can implement more complicated logic using the last params to
init():

window.onload = function() {
	Drag.init(document.getElementById("p"), null, null, 
		null, null, null, false, false, null, mySin);
}
function mySin(x) {
	return Math.round(Math.sin((x - 20) / 10) * 10) + 50;
}
