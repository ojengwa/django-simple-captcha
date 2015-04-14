# Django Simple Captcha #

## Configuration ##

The following configuration elements can be defined (in your `settings.py`)

#### `CAPTCHA_FONT_PATH` ####
Full path and filename of a TrueType (TTF), OpenType, or [pilfont](http://www.pythonware.com/library/pil/handbook/pilfont.htm) font file used to render text.

Defaults to: `fonts/Vera.ttf` (included in the application, GPL font).

Note that your PIL installation must support TTF and/or OpenFont if you want to use this kind of glyphs (most modern distributions of PIL do.)

#### `CAPTCHA_FONT_SIZE` ####
Font-size in pixels of the rendered text.

Defaults to `'22'`.


#### `CAPTCHA_LETTER_ROTATION` ####
A random rotation in this interval is applied to each letter in the challenge text.

Defaults to `(-35,35)`.

New in version 0.1.6: set this to None to disable letter roation.


#### `CAPTCHA_BACKGROUND_COLOR` ####
Background-color of the captcha. Can be expressed as html-style `#rrggbb`, `rgb(red, green, blue)`, or common html names (e.g. "red").

Defaults to: `'#ffffff'`

#### `CAPTCHA_FOREGROUND_COLOR` ####
Foreground-color of the captcha.

Defaults to `'#001100'`

#### `CAPTCHA_CHALLENGE_FUNCT` ####
String representing a python callable (i.e. a function) to use challenge generator.

See CaptchaGenerators for a list of available generators and a guide on how to write your own.

Defaults to: `'captcha.helpers.random_char_challenge'`


#### `CAPTCHA_NOISE_FUNCTIONS` ####
List of strings of python callables that take a PIL [DrawImage](http://www.pythonware.com/library/pil/handbook/imagedraw.htm) object and an [Image](http://www.pythonware.com/library/pil/handbook/image.htm) iamge as input, modify the DrawImage, then return it.

Defaults to: `('captcha.helpers.noise_arcs','captcha.helpers.noise_dots',)`

#### `CAPTCHA_FILTER_FUNCTIONS` ####
List of strings of python callables that take a PIL [Image](http://www.pythonware.com/library/pil/handbook/image.htm) object as input, modify it and return it.

These are called right before the rendering, i.e. after the noise functions.

Defaults to: `('captcha.helpers.post_smooth',)`

#### `CAPTCHA_WORDS_DICTIONARY` ####
Required for the `word_challenge` challenge function only. Points a file containing a list of words, one per line.

Defaults to: `'/usr/share/dict/words'`

#### `CAPTCHA_FLITE_PATH` ####
Full path to the `flite` executable. When defined, will automatically add audio output to the captcha.

Defaults to: `None` (no audio output)


#### `CAPTCHA_TIMEOUT` ####
Integer. Lifespan, in minutes, of the generated captcha.

Defaults to: `5`

#### `CAPTCHA_LENGTH` ####

Sets the length, in chars, of the generated captcha. (for the `'captcha.helpers.random_char_challenge'` challenge)

Defaults to: `4`


#### `CAPTCHA_DICTIONARY_MIN_LENGTH` ####

When using the `word_challenge` challenge function, controls the minimum length of the words to be randomly picked from the dictionary file.

Defaults to: `0`

#### `CAPTCHA_DICTIONARY_MAX_LENGTH` ####

When using the `word_challenge` challenge function, controls the maximal length of the words to be randomly picked from the dictionary file.

Defaults to: `99`

Note: it's perfectly safe to specify e.g. `CAPTCHA_DICTIONARY_MIN_LENGTH = CAPTCHA_DICTIONARY_MAX_LENGTH = 6` but it'd considered an error to define `CAPTCHA_DICTIONARY_MAX_LENGTH` to be smaller than  `CAPTCHA_DICTIONARY_MIN_LENGTH`.


#### `CAPTCHA_OUTPUT_FORMAT` ####

**New in version 0.1.6**

Specify your own output format for the generated markup, when e.g. you want to position the captcha image relative to the text field in your form.

Defaults to: ` u'%(image)s %(hidden_field)s %(text_field)s' `

Note: the three keys have to be present in the format string or an error will be thrown at runtime.