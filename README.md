# Work in Progress, public release on January 21th (Wordle-prick-day)

# More + Wordle = Mordle

## Wordle


Josh Wardle his Wordle, has taken the Internet by storm.

Soon people started building clones, my favorite is the [Welsh version](https://www.hiriaith.cymru/gairglo) weighing in at a whopping 2.2 MEGA Byte.

A fun one, is the [multi-player version](https://www.youtube.com/watch?v=uvCl39bemp0).

Best interview with Josh "Wordle" Wardle: https://slate.com/culture/2022/01/wordle-game-creator-wardle-twitter-scores-strategy-stats.html

Even Google joined the hype, with a [Wordle Easter-Egg](https://9to5google.com/2022/01/21/google-wordle-easter-egg/)


> The most important part might not be its game concept, but the fact that Josh built Wordle with Web Components.

## Web Components are Web Components are Web Components

The whole fun of native Web Components is reusability and extensibility. That means you can use the **ORIGINAL** source code (like a library) and **EXTEND** on it.

1 picture says more than words:

![](https://i.imgur.com/Taw5g55.png)



You DO need knowledge about HOW Web Components **function**. That is why I built my Qomponent Inspector.

But, still, I had challenges challenges. Josh did not provide documentation, and his source code is minified.



## Wordle has no license

And before you send me hate mail; here is the copyright from the Wordle source code:

![](https://i.imgur.com/b96worl.png)


## Building Mordle


I had heard of Wordle before, but I opened the site only after I heard it was created with Web Components technology.

So after guessing the word of the day, I hit F12 and dove into the source code.

Nothing unfamiliar to me, I have this "hackers" attitude since I first pressed the ESC key on a [TRS-80 Model-I](http://www.trs-80.org/model-1/) keyboard to change my high-scores. You can't blame me, I was 10.

Josh has done a decent job. He uses a hash to name his _one and only_ JavaScript file, so you can't easily link to it, and hijack his code.

I then ran my (personal) Qomponent Inspector on the code. This does a _dive_ into the DOM, and lists (the first used) copy of all used Web Components.

As you can see below, there isn't much Web Components going on. They are mainly used only to render content. The meat and bones of Wordle is in the `<game-app>` Web Component.

And it did not take long to spot a very interesting property! **gorge** was todays correct word!

![](https://i.imgur.com/h8ivuGz.png)

## Diving deeper, into the rabbit hole

I then dove deeper into the JavaScript source code, and quickly spotted **all** words are readable in the source code. Being a single JavaScript file, it is very easy to copy and **_change_** the original source code, and create your own (localized) version.

Too easy... I did that type of changes on BASIC sources way back in 1979 on that TRS-80

I could have rewritten the app with (slightly) better use of Web Components. But I wanted to keep the code as simple as possible, and I wanted to keep it as close to the original as possible.

Why, you ask? Because I wanted to make it as easy as possible to create **YOUR OWN** version of Wordle.

**Using Josh his original code!**

**100% of his original code!**




## Your own Wordle solution word

REMEMBER! I am absolultely **NOT** making ANY changes to Josh his JavaScript code!

Using Chromium Browser **sources/snippets** you need only a few lines of **standard JavaScript code** code to create you own ``<my-game>`` Web Component, which **extends** from Josh his original ``<game-app>`` Web Component.

![](https://i.imgur.com/Vhm0AVH.png)

## Wordle with a custom word in a JSFiddle

For a JSFiddle you copy all of Josh his JavaScript code (from one file) into the JavaSscript section.
Also copy the ``<STYLE>`` tag **content** from Josh his ``index.html`` file to the JSFiddle CSS section.

Then all HTML required is:

````html
<my-game></my-game>
<script>
  window.onload = function() {
    customElements.define(
      "my-game",
      class extends customElements.get("game-app") {
        connectedCallback() {
          super.connectedCallback();
          this.solution = "hacks"; 
          // click on title to removed saved state, play word again
          this.shadowRoot.querySelector(".title").onclick = localStorage.removeItem("gameState");
        }
      }
    ); 
  }
</script>
````

{% jsfiddle https://jsfiddle.net/WebComponents/x8eyv1f4 result,html,css,javascript %}

## Lessons learned:

- Web Components can be **extended** from **existing** Web Components. Most of us call this using a **BaseClass**

- Web Components can be created **after** definition in the DOM, all instances will automagically **upgrade**

But why stop there? I am not a 10 year old _scriptkiddie_ hacking away in BASIC anymore.

Let's up the ante. **Extend Wordle to play all past words**


## Overloading Josh his methods


The ``<game-app>.evaluateRow()`` method is called every time a new word is entered.	

* I can **add** my onw code by saving a reference the original method.
* declaring my own ``this.newEvaulateRow()`` method, 

````javascript
  // save original method
  this.savedEvaluateRowJoshCode = this.evaluateRow;
  // and overload with the new method
  this.evaluateRow = this.newEvaluateRow;
````

* and calling the original method.

````javascript
  newEvaluateRow() {
    let guessWord = this.boardState[this.rowIndex];
  this.savedEvaluateRowJoshCode(); // Josh's original code incs rowindex
 ````


## Make World auto play

For ease of use I copied Josh Wardle his **original** source code to Github

https://mordle.github.io/wordle_main_code.js

With some extra line of script I can now **autoplay** the game.

https://mordle.github.io/?sentence=danny,hacks,super,wordle,wordle,lingo,words


{% jsfiddle https://jsfiddle.net/WebComponents/bvmnujfg result,html,css,javascript %}

## What is your birtday Wordle?

With the source code available on Github, it is easy to extract Josh hist dictionaries

````javascript
  async readDictionary() {
    let source = await ( await fetch(__WORDLE_MAIN_SOURCE_CODE__) ).text();

    function extractByFirstWord(word) {
      let words = source
      .split(word)[1]
      .split("]")[0]
      .replaceAll('"', "")
      .replaceAll("\r", "")
      .replaceAll("\n", "")
      .split(",")
      .map((word) => word.trim());
      words[0] = word;
      return words;
    }
    this._wordlewords = extractByFirstWord("cigar");
    this._dictionary = extractByFirstWord("aahed");
  }
````

The Mordle can page back/foward to your birthday, and play the wordle:

https://mordle.github.io/?year=2022&month=1&day=21

Note: you may to clear the ``gameState`` in your browser's local storage to play again.

# Learning Web Components

Just play! play! play! You only learn this by doing.

And don't grab a tool and think you are done. 

Learn the technology first, then find yourself a tool that does the job better!

_A Fool with a Tool, is still a Fool_

But don't take this from me, I am just an old geezer who in 1979 hit the ESC key on a [TRS-80 Model-I](http://www.trs-80.org/model-1/), and learned to program.




