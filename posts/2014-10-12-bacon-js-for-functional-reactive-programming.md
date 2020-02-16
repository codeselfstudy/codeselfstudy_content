---
title: Bacon.js for Functional Reactive Programming
date: 2014-10-12
---

I'm at a presentation by <a href="http://blog.thepete.net/">Pete Hodgson</a> on <a href="http://en.wikipedia.org/wiki/Functional_reactive_programming">functional reactive programming</a> at Silicon Valley Code Camp, and he's covering <a href="http://baconjs.github.io/">Bacon.js</a>.<br /><br />Bacon.js:

<blockquote><div>A small functional reactive programming lib for JavaScript. Turns your event spaghetti into clean and declarative feng shui bacon, by switching from imperative to functional. It's like replacing nested for-loops with functional programming concepts like map and filter. Stop working on individual events and work with event-streams instead. Transform your data with map and filter. Combine your data with merge and combine. Then switch to the heavier weapons and wield flatMap and combineTemplate like a boss. It's the _ of Events. Too bad the symbol ~ is not allowed in Javascript.</div></blockquote>

Here are some more explanations:<br /><a href="http://raimohanska.github.io/bacon.js-slides/index.html">http://raimohanska.github.io/bacon.js-slides/index.html</a><br /><a href="http://philipnilsson.github.io/badness/">http://philipnilsson.github.io/badness/</a>

Here's a code example from the talk -- streams vs. variables:

```javascript
$(function () {
    var $slider = $('.slider input'),
        $label = $('.slider .label');

    $slider.asEventStream("input", inputEventToVal)
        .map(parseFloat)
        .map(function (x) {
            return Math.round(x*100);
        })
        .map(function (x) {
            return ""+x+"%";
        })
        .assign($label, "text");
});
```

Here's another partial example that sums the values from the two sliders:

```javascript
var summer = function (a, b) {
    return a + b;
};

var floatsFromSlider = function ($slider) {
    return $slider
        .asEventStream("input", inputEventToVal)
        .debounce(200) // not sure of the value here
        .map(parseFloat);
};

var streamA = floatsFromSlider($sliderA);
var streamB = floatsFromSlider($sliderA);
streamA.visualize("stream A");
streamB.visualize("stream B");
streamA.assign($labelA, "text");
streamB.assign($labelB, "text");
var combined = Bacon.combineWith(summer, streamA, streamB);
combined.visualize("combined");
combined.assign($summedLabel, "text");
```
