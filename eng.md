Look, I like good typography as much as the next person—maybe even a little
more. When a CSS property came along with promises to doctor all my type with 
ligatures and carefully calculated kerning—not some half-assed tracking, but 
real*kerning*—I jumped at it. I put `text-rendering: optimizeLegibility` on
headings, body copy, navigation links; I slapped it on images*just in case* a
ligature might appear in the background of a photograph, blurred, like an 
aesthetically satisfying poltergeist.

Truly, these were my web typography salad days; an era of copy littered with *
fi* and *fft* and—be still my heart—*st* ligatures. The letters of “water”
were themselves kerned water-tight, and I looked desperately for reasons to type
“AVAST” in all caps, as if to spite the jankily-kerned word I once knew.

![][1]

The differences between `text-rendering: optimizeLegibility` (left) and 
`text-rendering: auto` (right) are subtle, even for the keenly design-eyed.

In the back of my mind, though, I knew these newfound wings were made of wax.
All this typographic power came with a cost:
`text-rendering: optimizeLegibility` is slow—and by “slow,” I mean that
it can bog down an entire page, from initial render time to repaints. More than 
that, though, it’s*buggy*: Android in particular has [serious issues][2] trying
to render a page that uses`optimizeLegibility` heavily, especially the 
[older versions][3] that are still, sadly, very common today.

The bugs may not make much sense, but the speed issues do. There could be
thousands of tiny calculations involved in kerning a long run of text, and that 
puts a heavy strain on a device’s processor. In a modern desktop browser like 
Chrome, well,[it isn’t great][4], and on an underpowered mobile device it’s a
nightmare—especially when`@font-face` is in play. All the work that goes into
`optimizeLegibility` has to take place before type can be rendered at all,
meaning a drastically prolonged[Flash of Invisible Text][5] or a prolonged 
[Flash of Fallback Text][6], depending on the method used to load them.

![][7]

[WebPageTest.org][8]’s timeline view, using a throttled connection. The only
difference between these two pages is
`p { text-rendering: optimizeLegibility; }` and 
`p { text-rendering: optimizeSpeed; }`

The key, as you might expect, is moderation. Enabling these features on the
occasional subhed won’t do any serious performance harm; not*noticable* harm,
anyway.

In fact, the default setting of `text-rendering: auto` doesn’t always leave
us completely sans ligatures—pun intended—or with character spacings you could 
drive a truck through. In Firefox (and possibly[WebKit][9] and Blink,
eventually), any type with a`font-size` of `20px` or above is opted into 
`optimizeLegibility`’s features. On type that large the effects are much more
noticeable, and a few short runs of text aren’t apt to hurt our performance in 
any measurable way.

Of course, if we want to opt out of these features entirely, there’s always 
`text-rendering: optimizeSpeed`, which does away with `optimizeLegibility`’s
features—and costs—entirely, no matter the type size. I’m almost always willing 
to defer to the browser by keeping the default`text-rendering: auto` intact,
but if you find yourself working on a page with a healthy amount of text with a
`font-size` larger than 20px, you may want to finesse things a little with 
`text-rendering: optimizeSpeed`.

![][10] This entry was posted by [Mat Marquis][11] ([@wilto][12])  on May 13,
2015   in [CSS][13], [Performance][14] and [Feature][15].  

[Tweet][16]

 [1]: img/text-render_zoom.png
 [2]: http://stackoverflow.com/search?q=%5Bandroid%5D+optimizelegibility
 [3]: https://code.google.com/p/android/issues/detail?id=15067

 [4]: http://www.webpagetest.org/video/compare.php?tests=150429_5K_ZPS%2C150429_7C_ZPT&thumbSize=200&ival=1000&end=visual
 [5]: http://www.filamentgroup.com/lab/font-loading.html
 [6]: http://www.filamentgroup.com/lab/font-events.html
 [7]: img/wpt-text.png
 [8]: http://webpagetest.org
 [9]: https://bugs.webkit.org/show_bug.cgi?id=41363
 [10]: img/2d087e6ab3f067d53c6cbc2e9b722a62?s=80

 [11]: http://bocoup.com/weblog/author/mat-marquis/ "View all posts by Mat Marquis"
 [12]: http://twitter.com/wilto
 [13]: http://bocoup.com/weblog/category/css/ "View all posts in CSS"

 [14]: http://bocoup.com/weblog/category/performance/ "View all posts in Performance"
 [15]: http://bocoup.com/weblog/category/feature/ "View all posts in Feature"
 [16]: https://twitter.com/share