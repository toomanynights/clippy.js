Clippy.JS
=========

Add Clippy or his friends to any website for instant nostalgia.

This is a maintained fork of the original [Clippy.JS](https://github.com/clippyjs/clippy.js) by [Smore](https://web.archive.org/web/2020*/smore.com/clippy-js) (Fireplace, Inc.), with bugfixes and improvements.

### Changes from the original

- **Touch/mobile support** — drag Clippy on touchscreens (touchstart/touchmove/touchend)
- **Show/Hide animation timing** — fixed frame durations that were too fast to see (10ms → 75ms)
- **Show() positioning** — smart default placement (bottom-right) with fade-in, fixed operator precedence bug
- **Balloon positioning** — fixed scroll offset calculation for `position: fixed` elements
- **Balloon timing** — increased `CLOSE_BALLOON_DELAY` (2s → 5s), decreased `WORD_SPEAK_TIME` (200ms → 150ms)
- **Balloon speak()** — clears pending hide timeout before new speech
- **delay() scope** — fixed `this` context bug in the delay queue callback
- **Preview images** — added `preview.png` for each agent
- **No build directory** — use `src/` files directly (see usage below)


Usage: Setup
------------

Include the source files individually (no build step needed):

```html
<!-- Stylesheet -->
<link rel="stylesheet" type="text/css" href="clippy/src/clippy.css" media="all">

<!-- jQuery 1.7+ -->
<script src="jquery.min.js"></script>

<!-- Clippy.js source files (order matters) -->
<script src="clippy/src/queue.js"></script>
<script src="clippy/src/animator.js"></script>
<script src="clippy/src/balloon.js"></script>
<script src="clippy/src/agent.js"></script>
<script src="clippy/src/load.js"></script>

<!-- Override the default agent path if hosting locally -->
<script type="text/javascript">
    clippy.BASE_PATH = '/path/to/clippy/agents/';
</script>

<!-- Init -->
<script type="text/javascript">
    clippy.load('Clippy', function(agent){
        agent.show();
    });
</script>
```

By default, `clippy.BASE_PATH` points to `//s3.amazonaws.com/clippy.js/Agents/` (no longer available). Override it to point to your local `agents/` directory.


Usage: Actions
--------------

All agent actions are queued and executed in order, so you can stack them.

```javascript
// play a given animation
agent.play('Searching');

// play a random animation
agent.animate();

// get a list of all the animations
agent.animations();
// => ["MoveLeft", "Congratulate", "Hide", "Pleased", "Acknowledge", ...]

// Show text balloon
agent.speak('When all else fails, bind some paper together. My name is Clippy.');

// move to the given point, use animation if available
agent.moveTo(100,100);

// gesture at a given point (if gesture animation is available)
agent.gestureAt(200,200);

// stop the current action in the queue
agent.stopCurrent();

// stop all actions in the queue and go back to idle mode
agent.stop();
```

Available Agents
----------------

Bonzi, Clippy, F1, Genie, Genius, Links, Merlin, Peedy, Rocky, Rover


Special Thanks
--------------

* The original [Clippy.JS](https://github.com/clippyjs/clippy.js) project by Smore / Fireplace, Inc.
* [Cinnamon Software](http://www.cinnamonsoftware.com/) for [Double Agent](http://doubleagent.sourceforge.net/), used to unpack the original agent files
* Microsoft, for creating Clippy :)
