# Django Simple Captcha #

## Available Generators ##
The following generators are available:

### Random chars ###

Classic captcha that picks four random chars. This is case insensitive.

`CAPTCHA_CHALLENGE_FUNCT = 'captcha.helpers.random_char_challenge'`

![http://django-simple-captcha.googlecode.com/files/Random%20chars.png](http://django-simple-captcha.googlecode.com/files/Random%20chars.png)


### Simple Math ###

Another classic, that challenges the user to resolve a simple math challenge by randomly picking two numbers between one and nine, and a random operator among plus, minus, times.

`CAPTCHA_CHALLENGE_FUNCT = 'captcha.helpers.math_challenge'`

![http://django-simple-captcha.googlecode.com/files/Math.png](http://django-simple-captcha.googlecode.com/files/Math.png)



### Dictionary Word ###

Picks a random word from a dictionary file. Note, you must define `CAPTCHA_WORDS_DICTIONARY` in CaptchaConfiguration to use this generator.

`CAPTCHA_CHALLENGE_FUNCT = 'captcha.helpers.word_challenge'`

![http://django-simple-captcha.googlecode.com/files/Dictionary.png](http://django-simple-captcha.googlecode.com/files/Dictionary.png)




## Roll your own ##
To have your own challenge generator, simply point `CAPTCHA_CHALLENGE_FUNCT` to a function that returns a tuple of strings: the first one (the challenge) will be rendered in the captcha, the second is the valid response to the challenge, e.g. `('5+10=', '15')`, `('AAAA', 'aaaa')`

Sample generator that returns six random digits:
```
def random_digit_challenge():
    import random
    ret = u''
    for i in range(6):
        ret += str(random.randint(0,9))
    return ret, ret
```