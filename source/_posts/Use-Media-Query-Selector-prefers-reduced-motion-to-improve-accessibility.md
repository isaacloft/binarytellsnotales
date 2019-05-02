---
title: 'Use Media Query Selector: prefers-reduced-motion to improve accessibility'
date: 2019-05-02 09:53:07
tags: [frontend, accessibility]
categories: frontend
---

#### This article is more of a FYI for myself as the google doc is very thorough.

<i>"Animation on the web
Animation is oftentimes used to provide feedback to the user .......  there are decorative effects like animated gradients, parallax scrolling, background videos, and several others. While many users enjoy such animations, some users dislike them because they feel distracted or slowed down from them. In the worst case, users may even suffer from motion sickness as if it were a real life experience, so for these users reducing animations is a medical necessity." <i>

Articles I found useful: 
1. [On Google Developer Doc](https://developers.google.com/web/updates/2019/03/prefers-reduced-motion)
2. [CSS tricks](https://css-tricks.com/introduction-reduced-motion-media-query/)

<!--more-->

### Long story short
One simple implementation:

``` css
/*
  If the user has expressed their preference for
  reduced motion, then don't use animations on buttons.
*/
@media (prefers-reduced-motion: reduce) {
  button {
    animation: none;
  }
}

/*
  If the browser understands the media query and the user
  explicitly hasn't set a preference, then use animations on buttons.
*/
@media (prefers-reduced-motion: no-preference) {
  button {
    /* `vibrate` keyframes are defined elsewhere */
    animation: vibrate 0.3s linear infinite both;
  }
}
```

### To test this, we have to enable accessibility feature on devices, such as on Mac -> Accessibility -> Display -> Reduce Motion


