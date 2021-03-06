Nestable
========

## We are writing a new readme! Till now, please continue read the source ;)

## PLEASE NOTE

~~I cannot provide any support or guidance beyond this README. If this code helps you that's great but I have no plans to develop Nestable beyond this demo (it's not a final product and has limited functionality). I cannot reply to any requests for help.~~.

**I'm picking up active developement for Nestable! Pull requests are welcome!**

* * *

### Drag & drop hierarchical list with mouse and touch compatibility (jQuery / Zepto plugin)

[**Try Nestable Demo**](http://dbushell.github.com/Nestable/)

Nestable is an experimental example and IS under active development. If it suits your requirements feel free to expand upon it!

## Usage

Write your nested HTML lists like so:

    <div class="dd">
        <ol class="dd-list">
            <li class="dd-item" data-id="1">
                <div class="dd-handle">Item 1</div>
            </li>
            <li class="dd-item" data-id="2">
                <div class="dd-handle">Item 2</div>
            </li>
            <li class="dd-item" data-id="3">
                <div class="dd-handle">Item 3</div>
                <ol class="dd-list">
                    <li class="dd-item" data-id="4">
                        <div class="dd-handle">Item 4</div>
                    </li>
                    <li class="dd-item" data-id="5">
                        <div class="dd-handle">Item 5</div>
                    </li>
                </ol>
            </li>
        </ol>
    </div>

Then activate with jQuery like so:

    $('.dd').nestable({ /* config options */ });

### Events
`change`: For using an .on handler in jquery


### Methods

You can get a serialised object with all `data-*` attributes for each item.

    $('.dd').nestable('serialize');

The serialised JSON for the example above would be:

    [{"id":1},{"id":2},{"id":3,"children":[{"id":4},{"id":5}]}]

### On the fly nestable generation

You can passed serialized JSON as an option if you like to dynamically generate a Nestable list:

    <div class="dd" id="nestable-json"></div>

    <script>
    var json = '[{"id":1},{"id":2},{"id":3,"children":[{"id":4},{"id":5}]}]';
    var options = {'json': json }
    $('#nestable-json').nestable(options);
    </script>

NOTE: serialized JSON has been expanded so that an optional "content" property can be passed which allows for arbitrary custom content (including HTML) to be placed in the Nestable item

Or do it yourself the old-fashioned way:

	<div class="dd" id="nestable3">
		<ol class='dd-list dd3-list'>
			<div id="dd-empty-placeholder"></div>
		</ol>
    </div>
	
	<script>
	$(document).ready(function(){ 
		var obj = '[{"id":1},{"id":2},{"id":3,"children":[{"id":4},{"id":5}]}]';
		var output = '';
		function buildItem(item) {
		
		    var html = "<li class='dd-item' data-id='" + item.id + "'>";
		    html += "<div class='dd-handle'>" + item.id + "</div>";
		
		    if (item.children) {
		
		        html += "<ol class='dd-list'>";
		        $.each(item.children, function (index, sub) {
		            html += buildItem(sub);
		        });
		        html += "</ol>";
		
		    }
		
		    html += "</li>";
		
		    return html;
		}
		
		$.each(JSON.parse(obj), function (index, item) {
		
		    output += buildItem(item);
		
		});
		
		$('#dd-empty-placeholder').html(output);
		$('#nestable3').nestable();
	});
	</script>
	
### Configuration
You can change the follow options:

* `maxDepth` number of levels an item can be nested (default `5`)
* `group` group ID to allow dragging between lists (default `0`)

These advanced config options are also available:

* `listNodeName` The HTML element to create for lists (default `'ol'`)
* `itemNodeName` The HTML element to create for list items (default `'li'`)
* `rootClass` The class of the root element `.nestable()` was used on (default `'dd'`)
* `listClass` The class of all list elements (default `'dd-list'`)
* `itemClass` The class of all list item elements (default `'dd-item'`)
* `dragClass` The class applied to the list element that is being dragged (default `'dd-dragel'`)
* `handleClass` The class of the content element inside each list item (default `'dd-handle'`)
* `collapsedClass` The class applied to lists that have been collapsed (default `'dd-collapsed'`)
* `placeClass` The class of the placeholder element (default `'dd-placeholder'`)
* `emptyClass` The class used for empty list placeholder elements (default `'dd-empty'`)
* `expandBtnHTML` The HTML text used to generate a list item expand button (default `'<button data-action="expand">Expand></button>'`)
* `collapseBtnHTML` The HTML text used to generate a list item collapse button (default `'<button data-action="collapse">Collapse</button>'`)
* `json` JSON string used to dynamically generate a Nestable list. This is the same format as the `serialize()` output

**Inspect the [Nestable Demo](http://ramonsmit.github.io/Nestable/) for guidance.**

## Change Log

### 7th April 2014

* New pickup of repo for developement. 

### 15th October 2012

* Merge for Zepto.js support
* Merge fix for remove/detach items

### 27th June 2012

* Added `maxDepth` option (default to 5)
* Added empty placeholder
* Updated CSS class structure with options for `listClass` and `itemClass`.
* Fixed to allow drag and drop between multiple Nestable instances (off by default).
* Added `group` option to enabled the above.

* * *

Original Author: David Bushell [http://dbushell.com](http://dbushell.com/) [@dbushell](http://twitter.com/dbushell/)
New Author     : Ramon Smit    [http://ramonsmit.nl](http://ramonsmit.nl) [@Ram0nSm1t](https://twitter.com/Ram0nSm1t/)

Copyright © 2012 David Bushell / © Ramon Smit 2014 | BSD & MIT license
