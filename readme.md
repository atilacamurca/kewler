
# kewler

[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)

`kewler` is a simple functional and immutable color manipulation library.

## What does it mean?

Ok, there is quite a few color manipulation function, but they are all kinda object oriented when you create your object instance and manipulate it, this one is more like a functional one, where you create an immutable color wrapper which is a function and run any alteration you want and eventually get a hex color.

For example:

```js
import {color} from 'kewler';

const blue = color('#0593ff');
console.log(blue()); // Prints '#0593ff'
```

Cool, you have a blue color boxed and wrapped.

- _HOLD ON! You've just made a function which returns the values passed as first parameter, I can do it myself!!_

Ok sorry, that wrapper does a bit more... Want to get a darker one? Here you go:

```js
import {lightness} from 'kewler';

const lightBlue = blue(lightness(10));
console.log(lightBlue()); // Prints '#38a9ff'
```

Now you have another wrapper with a color 10% lighter!

- _An old senator that I met last week told me that the dark side is more cool, can I have it pls?_

Oh well you can do whatever you want with your wrapper now, want a darker one? Here you go:

```js
const darkLightBlue = lightBlue(lightness(-30));
console.log(darkBlue()); // Prints '#005a9e'
```

- _Hhhm nice, but color is a bit more than just light and dark... I'm just not gonna use your library if..._

Ok ok, you can change saturation and hue as well:

```js
import {saturation, hue} from 'kewler';

const paleBlue = blue(saturation(-50));
console.log(paleBlue()); // Prints '#5089b4'

const blueWhichIsActuallyGreen = blue(hue(-60));
console.log(blueWhichIsActuallyGreen()); // Prints '#05ff71'
```

And you can also combine and chain them:

```js
const pimpMyBlue = blue(saturation(-30), lightness(10));
console.log(pimpMyBlue()); // Prints '#56a5e1'

const blueWhichIsActuallyGreenButPaleAndLight = blue(hue(-60))(saturation(-30), lightness(10));
console.log(blueWhichIsActuallyGreenButPaleAndLight()); // Prints '#56e192'
```

Possibilities are literally endless!

```js
const ohMyBlue = blue(lightness(-10), hue(-30), lightness(5))(saturation(-20), hue(10))(lightness(20));
console.log(ohMyBlue()); // Prints '#63e0ee'
```

- _Woah! That's quite a lot of parenthesis!_

Oh sorry, I got a bit overexcited, my point is that you can create your wrapper and manipulate your wrapper as much as you want, all you have to remember is that __a color wrapper is always going to return another color wrapper if you pass it an argument__ (an alteration), and __it's always going to return a hex color when you execute it without any argument__.

That little wrapper that you get, you can pass it everywhere you want and modify it where you want, it's __[immutable](https://en.wikipedia.org/wiki/Immutable_object)__ and will return either a new wrapper or a HEX color value.

Writing your own alteration for a color is quite easy as well, an alteration is just a function that takes an [HSL color](https://css-tricks.com/yay-for-hsla/) value as an array and returns a new one:

```js
const myAlteration = ([hue, sat, lit]) => ([hue, sat - 30, lit + 10]);

const myNewBlue = blue(myAlteration);
console.log(myNewBlue); // Prints '#56a5e1'
```

Also, if you just want a one-off alteration on anything you can use the `color` function with more than one argument:

```js
const oneOffLightBlueFromHex = color('#0593ff', lightness(10));
console.log(oneOffLightBlueFromHex); // Prints '#38a9ff'

const oneOffLightBlueFromColor = color(blue(), saturation(-30), lightness(10));
console.log(oneOffLightBlueFromColor); // Prints '#56a5e1'
```

Ah and another thing (last one, I promise), you can use pass HSL values as an array (`[int, int, int]`) or an object (`{ hue: int, sat: int, lit: int }`):

```js
const blueFromHSLArray = color([206, 100, 51]);
console.log(blueFromHSLArray()); // Prints '#0593ff'

const blueFromHSLObject = color({hue: 206, sat: 100, lit: 51});
console.log(blueFromHSLObject()); // Prints '#0593ff'
```

I think that's it! Now have fun and enjoy a colorful life!

- _Hold on bloody american! That's not quite the right way of spelling 'colour', you should be a bit more respectful with our ~~British~~ English language!_

Ah, mmh, [I'm not american at all](http://adriantoine.com/about-me), I just thought that in IT, the american way of spelling english is more common, but as I'm currently living in England, I made a proxy `colour`, just for you!

```js
import {colour} from 'kewler';

const blue = colour('#0593ff');
console.log(blue()); // Prints '#0593ff'
```

Ok now that's it, enjoy!

- _No no no! You can't get away like this! Your library always returns a HEX value, but I need a HSL/RGB/Somethingelse value for my application!_

Well, I want to keep it simple and I think that most browsers and system support HEX color values, so that's why library returns it, if you want to stay functional, there are tons of converters which will convert HEX values to any other system, if you think returning HEX values is not a good choice, I'd love to discuss about it in a Github issue. You can also use another color manipulation library like [TinyColor](https://github.com/bgrins/TinyColor) (I have never used it, it's just the first result from Google).

My library also doesn't support transparency, but that's something I'm looking at.

Ok so just before going, here is the command to install it:

```console
$ npm install --save kewler
```

Have fun!