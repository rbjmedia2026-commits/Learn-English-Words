# Five a Day

A small browser game for learning English vocabulary: five words at a time, then a quick quiz to make them stick.

Everything is in one file, `index.html`. There is nothing to install, no account, and no server. Open the file in a browser and play.

## What it does

- **Four levels:** Entry, Mid, Expert and Pro. Pro words are rare words you mostly hear from professional speakers and writers, such as *ubiquitous*, *obfuscate* and *perspicacious*.
- **Two sources for new words:**
  - **Word list:** a built-in list of 695 checked words (182 Entry, 227 Mid, 141 Expert, 145 Pro).
  - **Fresh online:** new words fetched from free online dictionaries for each lesson.

  Either way, you never get the same new word twice.
- **5 words at a time.** Each word has its meaning, part of speech, an example sentence, a similar word, and a Listen button for pronunciation.
- **A quiz after each lesson** with six kinds of questions: choose the meaning, choose the word, fill in the blank, listen and choose, spell it with letter tiles, and a final matching round.
- **Second chances:** a wrong answer shows the right one, and the question comes back at the end.
- **New words whenever you like:** tap **New words** for a different five at any time, as often as you want. Tap **Undo** to bring back the words you had before; you can undo several steps.
- **Retake any quiz:** take the quiz again on a set as many times as you like.
- **Streaks, XP, ranks and stars** to keep it fun. A day counts toward your streak when you finish at least one quiz that day.
- **A word book** with every word you've learned. You can search it, filter it by level, and see a mastery score for each word.
- **Review mode** that quizzes you on the words you find hardest.
- **A downloadable review report:**
  - a printable HTML page with your stats, the words to practise, and every word you've learned
  - or a CSV file for Excel or Google Sheets
- Works on phones and computers, in light and dark mode, and with a keyboard (number keys to answer, Enter to continue, type letters to spell).

## How to play

Open `index.html` in Chrome, Safari, Edge or Firefox. Choose a level and where new words should come from. Your five words appear right away: tap **New words** if you already know them, or **Start learning** to begin.

Progress is saved in that browser on that device. This includes your streak, the words you've learned, XP, your undo history and any fresh words you've fetched. Clearing the browser's data resets it, and progress doesn't move between devices.

## Fresh words online

With **Fresh online** selected, each new set of words works like this:

1. The game asks the [Datamuse API](https://www.datamuse.com/api/) for real English words. It sorts them by how common they are, which decides the level: common words are Entry, rare words are Pro.
2. It looks up each word in the [Free Dictionary API](https://dictionaryapi.dev/), which uses Wiktionary data, to get a meaning and an example sentence.
3. It keeps only words that have an example sentence that uses the word. It skips any definition that describes the word as offensive, vulgar, slang, archaic or similar.

Both services are free and need no key, but they do need an internet connection. If they can't be reached, the game takes the words from the built-in list and says so. Fetched words are saved with your progress, so they appear in your word book and report and are never offered as new again.

Meanings and examples from the online dictionaries are written by their contributors, not checked by this project, so their quality varies more than the built-in list. You can change how common a word must be for each level in the `FREQ` setting in `index.html`.

## Share it with friends

The easiest way to give friends a link is to put `index.html` on a free static host, such as GitHub Pages, Netlify or Cloudflare Pages. Because the file is named `index.html`, the host serves it at the site's main address. Each person who opens the link gets their own progress in their own browser.

## Change the built-in words

The word list is the `WORDS_RAW` array near the bottom of `index.html`. Each entry looks like this:

```js
["abundant","adjective","existing in large amounts; more than enough","Fresh fruit is abundant at the market in summer.","plentiful","mid"],
```

The fields are: word, part of speech, meaning, example sentence, similar word (can be `""`), level.

A few rules keep the quiz fair:

- **Example:** the example sentence must contain the word exactly as written, because the fill-in-the-blank question removes it.
- **Meaning:** the meaning should not contain the word itself.
- **Part of speech:** must be one of `noun`, `verb`, `adjective`, `adverb`, `phrasal verb`, `idiom`.
- **Level:** must be one of `entry`, `mid`, `expert`, `pro`.
- **Near-synonyms:** if two words mean almost the same thing, add them to the `CLOSE` list so one is never offered as the wrong answer for the other.

Each level has a fixed shuffled order, and words you've already been shown aren't offered again until the level's list runs out. You can add new words at any time without breaking anyone's progress. 
## Optional Claude features

Code that mentions `window.claude` only runs when the page is opened inside Claude. There it:

- saves progress to the viewer's account
- has Claude write the fresh words, because pages inside Claude can't reach other websites
- saves reports through Claude's download prompt
- uses the Claude voice

Everywhere else, the game uses the browser's storage, the online dictionaries, a normal download and the device's built-in voice.

## Credits

- **Fonts:** [Young Serif](https://fonts.google.com/specimen/Young+Serif) and [Atkinson Hyperlegible](https://fonts.google.com/specimen/Atkinson+Hyperlegible), both under the SIL Open Font License, loaded from Google Fonts. Without an internet connection the game uses system fonts.
- **Fresh words:** the Datamuse API and the Free Dictionary API (dictionaryapi.dev, with data from Wiktionary under CC BY-SA). Their data is fetched while you play and is not part of this project.

## License

MIT. See `LICENSE`. This covers the code and the built-in word list.
