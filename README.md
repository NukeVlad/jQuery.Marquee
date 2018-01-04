jQuery-Marquee с поддержкой CSS3
==============

A **5.56 KB** (minified) 
Плагин jQuery для прокрутки текста, замена, устаревшего традиционного тэга marquee

Установка:
----
 - **NPM:** `npm install jquery.marquee --save`
 - **CDN:** [jsdelivr.com](http://www.jsdelivr.com/#!jquery.marquee)
```html
<script src="//cdn.jsdelivr.net/npm/jquery.marquee@1.5.0/jquery.marquee.min.js" type="text/javascript"></script>
```
- **Bower**: `bower install jQuery.Marquee`
- **Скачать:** [zip](https://github.com/aamirafridi/jQuery.Marquee/archive/master.zip)

Links:
-----
 - **Demo:** http://aamirafridi.com/jquery/jquery-marquee-plugin#examples
 - **jsFiddle:** http://jsfiddle.net/aamir/jc7F3/285/ to help you explain any issues you might face.

Опции:
--------
 - **allowCss3Support** Если вы хотите, чтобы плагин всегда анимировал, используя метод анимации jQuery, если браузер не поддерживает анимацию CSS3. По умолчанию ```true```
 - **css3easing** Работает, когда ```allowCss3Support``` is set to ```true``` - полный список см.: http://www.w3.org/TR/2013/WD-css3-transitions-20131119/#transition-timing-function . По умолчанию ```'linear'```
 - **easing** Требует плагин jQuery для замедления http://gsgd.co.uk/sandbox/jquery/easing/. По умолчанию ```'linear'```
 - **delayBeforeStart** Время в миллисекундах перед тем, как строка начинает анимацию. По умолчанию ```1000```
 - **direction** Направление, по которому будет выполнено движение ```'left' / 'right' / 'up' / 'down'```. По умолчанию ```'left'```. Примечание: нужно изменить это на ```ltr/rtl``` и т.д
 - **duplicated** Если объект нужно дублировать, чтобы показать эффект непрерывного потока. Используйте это только в том случае, если текст короче контейнера. По умолчанию ```false```
 - **duration** Продолжительность в миллисекундах, если вы хотите, чтобы ваш элемент перемещался. По умолчанию ```5000```.
 - **speed** Скорость будет превышать длительность. Скорость позволяет установить относительно постоянную скорость независимо от ширины содержащего элемента. Скорость измеряется в пикселях в секунду.
 - **gap** Разрыв в пикселях между тикерами. Будет работать только тогда, когда ```duplicated``` параметр ```true```. По умолчанию ```20```. Учтите: ```20``` означает ```20px``` поэтому нет необходимости указывать ```'20px'``` как значение.
 - **pauseOnHover** On hover pause the marquee. If browser supports CSS3 and ```allowCss3Support``` is set to ```true``` than it will be done using CSS3. Otherwise this will be done using jQuery plugin https://github.com/tobia/Pause. Default is ```false```. Check the demo page for a demo.
 - **pauseOnCycle** On cycle, pause the marquee for ```delayBeforeStart``` milliseconds.
 - **startVisible** The marquee will be visible in the start if set to `true`. Thanks to @nuke-ellington 👍

Events:
------
 - **beforeStarting:** Event will be fired on the element before animation starts.
 - **finished:** Event will be fired on the element after the animation finishes.
 - **paused:** Event will be fired on the element when the animation is paused.
 - **resumed:** Event will be fired on the element when the animation is resumed.

Methods:
---------------

These methods can be used like this:

 - First initialize marquee with any options ``` var $mq = $('.marquee').marquee();```
 - Then at any time you can call following methods ```var $mq.marquee('NAME-OF-METHOD-AS-STRING');```

Here is the list of all methods:

 - **pause**: To pause the marquee at any time.
 - **resume**: To resume the marquee after being paused previously.
 - **toggle**: To toggle between pause and resume methods.
 - **destroy**: To remove marquee plugin from your element. This method is useful if you are loading/changing the data using Ajax or just another string. You can combine this with ```finished``` event so you can let marquee to show some data and soon it finishes showing, you can destroy it, change the html and than apply the plugin again. See the demo page for details (links provided above).

Usage:
----

###HTML:

```html
<div class='marquee'>Lorem ipsum dolor sit amet, consectetur adipiscing elit END.</div>
```

or use this if you want to start the plugin with no options but want to use data attributes. You can use all the options listed above as data attributes. This is how you can use them:

```html
<div class='marquee' data-duration='5000' data-gap='10' data-duplicated='true' >
    Lorem ipsum dolor sit amet, consectetur adipiscing elit END.
</div>
```


###CSS:
```css
.marquee {
  width: 300px; /* the plugin works for responsive layouts so width is not necessary */
  overflow: hidden;
  border:1px solid #ccc;
}
```

###How to apply plugin:
```javascript
/**
 * Example of starting a plugin with options.
 * I am just passing some of the options in the following example.
 * you can also start the plugin using $('.marquee').marquee(); with defaults
*/
$('.marquee').marquee({
	//duration in milliseconds of the marquee
	duration: 15000,
	//gap in pixels between the tickers
	gap: 50,
	//time in milliseconds before the marquee will start animating
	delayBeforeStart: 0,
	//'left' or 'right'
	direction: 'left',
	//true or false - should the marquee be duplicated to show an effect of continues flow
	duplicated: true
});
```

###How to use methods:

```javascript
var $mq = $('.marquee').marquee();
$('.someLink').click(function(){
  $mq.marquee('pause/resume/toggle');
});
```

Change content and re-apply the plugin.
Check demo page for example: http://aamirafridi.com/jquery/jquery-marquee-plugin#examples
```javascript
$('.marquee')
	.bind('finished', function(){
		//Change text to something else after first loop finishes
		$(this).marquee('destroy');
		//Load new content using Ajax and update the marquee container
		$(this).html('Some new data loaded using ajax')
			//Apply marquee plugin again
			.marquee()
	})
	.marquee();

```

###How to use events:

Check demo page for example: http://aamirafridi.com/jquery/jquery-marquee-plugin#examples

```javascript
$('.marquee')
    .bind('beforeStarting', function () {
        //code you want to execute before starting the animations
    })
    .bind('finished', function () {
        //code you want to execute before after each animation loop
    })
    //Apply plugin
    .marquee({
        duration: 2000
    });
```

---

Images:
------
If you are using images in marquee, sometimes the plugin cannot calculate accurate widths while images are still loading. You can try this instead of ```$(document).ready(function(){...})```

```javascript
//if you have images in marquee
$(window).load(function() {
    $('.marquee').marquee();
});
```
----


Updates:
-----------

**Update (8 Mar 2016):**
Now plugin have new option: **startVisible** The marquee will be visible in the start if set to `true`. Thanks to @nuke-ellington 👍

**Update (24 Jan 2014):**

**Note: people who been asking me how to use this plugin with content being loaded with Ajax, please read notes about this update.**

 - New methods added, so now after you start the plugin using ```var $mq = $('.marquee').marquee();```, then you can pause, resume, toggle(pause, resume) and destroy methods e.g to remove the marquee plugin from your element simply use ```$mq.marquee('destroy');```. Similarly you can use pause the marquee any time using ```$mq.marquee('pause');```.
 - If you want to use use **Ajax** with this plugin i.e you want to change the content after you apply this plugin, please see the examples in demo page (link provided below).

 - Also made some changes so this plugin works with old versions of jQuery. I have tested it with jQuery 1.3.2 but quite sure it should work with some previous versions of jQuery.

**PLEASE report any bugs you find.**

For details please check the demos at: http://aamirafridi.com/jquery/jquery-marquee-plugin#examples

**Update (20 Dec 2013):**
Now the plugin will detect if browser supports CSS3 animations than it will animate the element using CSS3 which will perform much better than animating using jQuery.

The ```pauseOnHover``` also works using CSS3. The plugin just prepares the setup and required CSS3 animation CSS.

Due to some reasons if you want plugin to animate always using jQuery than you need to set ```allowCss3Support``` option to ```false```. Also an extra option ```css3easing``` is added.

Check demo page for example: http://aamirafridi.com/jquery/jquery-marquee-plugin#examples


**Update (27 Nov 2013):**
Easing option added. Requires jQuery easing plugin.


**Update (22 Nov 2013):**
Now plugin supports the 'up' and 'down' directions. Please have a look at the example to see how to use.


**Update (21 Aug 2013):**
If you want to hide the marquee for certain devices, try using ``` visibility: hidden``` with ``` height: 0``` & ```position: absolute``` instead of ``` display: none``` because jQuery cannot calculate with width etc of hidden elements.
For more details:
 - https://github.com/aamirafridi/jQuery.Marquee/issues/9
 - http://stackoverflow.com/questions/1841124/find-the-potential-width-of-a-hidden-element


**Update (22 Feb 2013):**
```pauseOnHover``` option added. Please note that you will need to include jQuery pause plugin: https://github.com/tobia/Pause before the jQuery Marquee plugin.


**Update (20 Feb 2013):**
 - The plugin is improved to adjust the speed according to the length of the text automatically. For more details read: https://github.com/aamirafridi/jQuery.Marquee/issues/1
 - 'duplicated' option added. See the details below in Options section.
