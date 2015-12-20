---
layout: post
title:  "Affix Flickering Problem in Bootstrap"
date:   2014-12-26 08:22
categories: webdev
comments: true
disqus_id: "bootstrap_affix_flickering"
---
## The Problem ##

As of the current version of [Bootstrap](http://getbootstrap.com/)
(V3.3.1) there exists an issue with Affix function and vertical
scrolling. For certain vertical sizes of the document inside the
browser window, scrolling down will have a flickering effect on the
content. This happens right when the Affix element is supposed to
stick to its position; instead you are met with an ugly scrolling
action. You can see this behavior below.

<div class="media-flex" style="padding-bottom: 71.7348927875%;">
  <img class="gfyitem img-pad img-center radius20" data-id="DescriptiveHeartyBrownbutterfly" data-dot="false" alt="Bootstrap Affix Vertical Scroll Flickering" />
</div>


Here's the code used to capture the behavior above:
<http://codepen.io/anon/pen/raMJox>. If you adjust the height of the
browser to the right size you should be able to replicate this issue.

## Diving Into Behavior ##

Affix works by replacing CSS classes on the Affix element when you
scroll past certain offset. In the example code above, the top offset
is set to 100px in `affix` function because that's the height of the
Header and we want the NavBar to stick to the top after you scroll
100px down, past the header.

```js
$(".nav").affix({
  offset: {
    top: 100
  }
});
```

When scrolling the document down exceeds the specified offset,
Bootstrap adds the CSS class `affix` to the Affix element. If you look
at the CSS code for `.affix` class you can see that the CSS property
`position` is set to `fixed`.

<img class="center-image" src="/assets/bootstrap-affix-flickering.png"
alt="Affix CSS Class">

When an element is set to fixed, it's removed from the regular flow of
the layout in the browser. The space that the NavBar occupied in the
original document is now gone. If the document height was 500px to
begin with and the NavBar occupied 100px of it, after we make NavBar
element fixed, the document height will become 400px.

You can check out this effect here:
<http://codepen.io/anon/pen/QwKKwv>. Click the button in the NavBar to
see the original height of the document. Scroll down until the NavBar
is fixed on top and then click on the button again to see the document
height. They should be different.

This document height re-adjustment causes an issue with Affix
function. Even though we just passed the 100px top offset and the
`affix` CSS class was added to the NavBar element, Affix function
recalculates the current scroll position and finds that it's less that
100px because of the removal of NavBar element from the layout due to
fixed positioning. Bootstrap removes `affix` CSS class and adds back
`affix-top` class to the NavBar element, which removes it from fixed
position and adds it back to the document layout. But adding NavBar
back to regular document flow increases the height of the document
again and the new scroll position is past 100px now which means
Bootstrap will add `affix` CSS class back to NavBar element. This back
and forth addition and removal of `affix` and `affix-top` CSS classes
on NavBar causes the flickering issue.

## The Fix ##

The fix is really simple. We just need to reserve the space in the
original document layout for the Affix element no matter what type of
positioning the Affix element has. Surround the Affix element with a
div or any other block element having a height equal to the Affix
element height. You can use either CSS or JavaScript to set the height
of the wrapping element.

**Option 1**
Source: <http://codepen.io/anon/pen/ogzqvo>

```html
<div class="nav-wrapper">
  <div class="nav"> NavBar </div>
</div>
```

```css
.nav-wrapper, .nav {
  height: 60px;
}
```

```js
$(".nav").affix({
  offset: {
    top: 100
  }
});
```

**Option 2**
Source: <http://codepen.io/anon/pen/YPGaKa>

```html
<div class="nav-wrapper">
  <div class="nav"> NavBar </div>
</div>
```

```js
$(".nav").affix({
  offset: {
    top: 100
  }
});

$(".nav-wrapper").height($(".nav").height());
```

**Note:** If you have some other scripts that manipulate your Affix
elements' height, make sure to run them before you set the height on
the wrapping element.

<script>
(function(d, t) {
var g = d.createElement(t),
s = d.getElementsByTagName(t)[0];
g.src = '/js/gfyajax-0.517d.js';
s.parentNode.insertBefore(g, s);
}(document, 'script'));
</script>
