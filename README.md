# Final Project Assignment 2: Explore One More! (FP2) 
DUE March 30, 2015 Monday (2015-03-30)

This is just like FP1, but where you do a different library. (Full description of FP1 is [on Piazza.][piazza])

During this assignment, you should start looking for teammates. See the project schedule [on Piazza.][schedule]

Write your report right in this file. Instructions are below. You can delete them if you like, or just leave them at the bottom.
You are allowed to change/delete anything in this file to make it into your report. It will be public.

This file is formatted with the [**markdown** language][markdown], so take a glance at how that works.

This file IS your report for the assignment, including code and your story.

Code is super easy in markdown, which you can easily do inline `(require net/url)` or do in whole blocks:
```
#lang racket

(require net/url)
```

### My Library: (library name here)
Write what you did!
Remember that this report must include:
 
* a narrative of what you did
* the code that you wrote
* output from your code demonstrating what it produced
* any diagrams or figures explaining your work 
 
The narrative itself should be no longer than 350 words. Yes, you can add more files and link or refer to them. This is github, handling files is awesome and easy!

Ask questions publicly in the Piazza group.

### How to Do and Submit this assignment

1. To start, [**fork** this repository][forking].
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning)
  3. (You may need to clone and push if you want to add extra files)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[schedule]: https://piazza.com/class/i55is8xqqwhmr?cid=453
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request
[The-Racket-G-I-T]: http://docs.racket-lang.org/gui/windowing-overview.html

###	The Racket Graphical Interface Toolkit

This library that I worked on can be found hear [**The Racket Graphical Interface Toolkit**][The-Racket-G-I-T]
I played around with frames, panels, and buttons. I changed some code given in the library I used to come up with two frames. One frame for a Calendar with a synchronization Button when clicked. It does not actually do the synchronization just gives a message to show that something happened when the Click to Sync button is pressed. It shows that calendar has been synched with the Map frame.
I made changes to another code provided to change to panel view on the canvas making the calendar canvas ever so slightly different from the map frame. The calendar frame has two buttons made in the horizontal panel that when clicked will display a massage to either show next month or the previous month. I also did play with mouse pointer event on the canvas and keyboard event if any of these two events do take place they would trigger as a massage on the canvas showing which event happened. I took a look at pausing button which when clicked takes over the frame no other event can take place until pause event is over in mine I put 15seconds.
 


### The Code that i played with :
```
#lang racket
;Norman Mutunga
;FP2
(require racket/gui/base)

;This creates or instantiates the frame with the label given "Normans"
;(define frame (new frame% [label "Normans"]))
;This part is like display it shows whats in the frame.
;(send frame show #t) ;#t to show the frame
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;Begin Frames ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;main frame for Google map 
(define frameM (new frame% [label "Google map"]))
;,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,>>>
;main frame created for the calender
(define frameC (new frame% [label "CalenderMap"]))
;;basic label
(define msgC (new message% [parent frameC]
                 [label " Syncronize Travel/Arrival Time /Due"]))
;; Button to be clicked to triger an event.
;it creates this on REP : (object:button% ...)
(new button% [parent frameC]
     [label "Click to Sync"]
     [callback (λ (button event)
                 (send msgC set-label "Callender Syncronized with map"))])
;,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,>>>
;;basic label
(define msgM (new message% [parent frameM]
                 [label "Type Of Map"]))
;; Button to be clicked to triger an event.
;it creates this on REP : (object:button% ...)
(new button% [parent frameM]
     [label "NeedDropDown to choose MapType"]
     [callback (λ (button event)
                 (send msgM set-label "Map Type/gotten/to/sync/with/calender"))])

;;;;;;;;;;Run the project;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
;;show calender
(send frameC show #t)
;;show the map
;(send frameM show #t)
;,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,End Frames,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
;,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,Canvas Begin,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
;; A drowing Canvas.
;,,,,,,,,,,Calender Canvas
(define my-calender-canvas%
  ;The base class is canvas%
  (class canvas%
    ; define an overiding methode to handle mouse events on Calender
    (define/override (on-event event )
      (send msgC set-label "Canvas Mouse"))
    ;define overriding methode to handle keyboard events
    (define/override (on-char event)
      (send msgC set-label "Canvas Keyboard"))
    ; call the superclass init , passing on all init args 
    ( super-new )))
;,,,,,,,,,,,,My Map Canvas,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
(define my-map-canvas%
  ;The base class is canvas%
  (class canvas%
    ; define an overiding methode to handle mouse events on Map
    (define/override (on-event event )
      (send msgM set-label "Canvas Mouse"))
    ;define overriding methode to handle keyboard events
    (define/override (on-char event)
      (send msgM set-label "Canvas Keyboard"))
    ; call the superclass init , passing on all init args 
    ( super-new )))
;,,,,,,,,,,,,,,End of Map Canvas,,,,,,,,,,,,,,,,,,,,,,,,
;make a canvas that handles events in the frame
;Sets Canvas for Calender
;it creates this on REP :(object:my-canvas% ...)
(new my-calender-canvas% [parent frameC])
;Sets Canvas for Map
;it creates this on REP :(object:my-canvas% ...)
(new my-map-canvas% [parent frameM])
;,,,,,,,,,,,,,,,,,,,,,,,,,,canvas End,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
;,,,,,,,,,,,This will pause for 5 seconds the entire frame,,,,,,,,
;it creates this on REP : (object:button% ...)
(new button% [ parent frameM]
     [label "Pause"]
     [callback (λ (button event) (sleep 15))])
;,,,,,,,,,,,,,End of Pause on Map,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
;,,,,,,,,,,,,Design the Calender,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,
;Creates a new Horizontal panel buttons in Calender,,,,,,,,,,
(define panelC (new horizontal-panel% [parent frameC]))
;;Left Button
(new button% [parent panelC]
     [label "Previous"]
     [callback (λ (button event )
                 (send msgC set-label "Previous Month"))])
;;Right Button
(new button% [parent panelC]
     [label "Next"]
     [callback (λ (button event )
                 (send msgC set-label "Next Month"))])
;,,,,,,,,,,,,,,,,,end of panel,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,



```


### Out Put From the code on the REPL:

```
(object:button% ...)
(object:button% ...)
(object:my-calender-canvas% ...)
(object:my-map-canvas% ...)
(object:button% ...)
(object:button% ...)
(object:button% ...)
> 
```
### Out Put Frames that have been resized 
 I am not able to find a way to show the visual out put on this platfoarm . 
