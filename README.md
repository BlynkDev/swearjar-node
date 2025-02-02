# swearjar-extended2

This is a modified version of [swearjar-extended](https://github.com/ahmedengu/swearjar-node)

Profanity detection and filtering library.

[![Build Status](https://travis-ci.org/raymondjavaxx/swearjar-node.svg?branch=master)](https://travis-ci.org/raymondjavaxx/swearjar-node)

## Installation

    npm install --save swearjar-extended2

## Usage

### swearjar.setLang(text)

Sets a language to load a dictionary of words to be used as filter.

| Language                                                 | Code              |
| -------------------------------------------------------- | ----------------- |
| [English](lib/config/en.json)                            | en                |
| [Filipino](lib/config/ph.json)                           | ph                |
| [Spanish](lib/config/es.json)                            | es                |
| [Bahasa](lib/config/id.json)                             | id                |

NOTE: A US English default list located in the config directory is included and loaded by default.

    var swearjar = require('swearjar-extended2');
    swearjar.setLang("en");

A dictionary is just a plain JSON file containing an object where its keys are the words to check for and the values are arrays of categories where the words fall in.

```
{
  "regex": {
    "\\w*fuck\\w*": [
      "category1",
      "category2"
    ],
    "word2": [
      "category1"
    ],
    "word3": [
      "category2"
    ]
  },
  "simple": {
    "word1": [
      "category1",
      "category2"
    ],
    "word2": [
      "category1"
    ],
    "word3": [
      "category2"
    ]
  },
  "emoji": {
    "1f4a9": [
      "category1",
      "category2"
    ],
    "word2": [
      "category1"
    ],
    "word3": [
      "category2"
    ]
  }
}
```


### swearjar.profane(text)

Returns true if the given string contains profanity.

    var swearjar = require('swearjar-extended2');
    swearjar.profane("hello there"); // false
    swearjar.profane("fuck you john doe"); // true

### swearjar.censor(text)

Replaces profanity with asterisks.

    var clean = swearjar.censor("fuck you john doe bitch"); // **** you john doe *****

### swearjar.words(text)

Get the words alongside there categories.

    swearjar.words('fuck you john doe'); // { fuck: ['sexual'] }
    
### swearjar.detailedProfane(text)

Get the words alongside there categories, count and censor the text.

    swearjar.detailedProfane('fuck you john doe')

returns:    
```
{
  categoryCount: {
    sexual: 1
  },
  censored: '**** you john doe',
  profane: true,
  wordCount: {
    fuck: 1
  },
  words: {
    fuck: [
      'sexual'
    ]
  }
}
```

### swearjar.scorecard(text)

Generates a report from the given text.

    swearjar.scorecard("fuck you john doe bitch fuck"); // {sexual: 2, insult: 1}

### swearjar.addRegex(text)

Add a regex.

    swearjar.addRegex('addedword?\\b', ['detected']);

### swearjar.addSimple(text)

Add a simple word.

    swearjar.addSimple('addedword', ['detected']);

### swearjar.addEmoji(text)

Add an emoji word.

    swearjar.addEmoji('1f596', ['detected']);


## Acknowledgements

`swearjar-node` is based on [Swearjar](https://github.com/joshbuddy/swearjar) (Ruby) and [Swearjar PHP](https://github.com/raymondjavaxx/swearjar-php).

## Sources
* [filipino-badwords-list](https://github.com/jromest/filipino-badwords-list)
* [Shutterstock](https://github.com/LDNOOBW/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words)
* [NLP_bahasa_resources](https://github.com/louisowen6/NLP_bahasa_resources)
