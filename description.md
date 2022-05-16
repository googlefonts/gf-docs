# Description file
{:.no_toc}

> <span class="icon">🦉</span>  `DESCRIPTION.en_us.html` contains the information that appears in the `#About` section on any specimen page of [Google Fonts](https://fonts.google.com) in order to give further information about the font family.
> This file will be created by the team member who will be onboarding the font. Thus the actual file a designer should write carefully would be the [README.md](readme.md) file as the information provided in it is crucial to building a good About section.

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Requirements

-   **The text length** should be around 500 words, and more than 100 characters.
-   **Allowed HTML elements:** `a`, `em`, `i`, `strong`, `b`, `p`, `ol`, `ul`, `li`.
-   **Other HTML elements**, especially inline CSS, classes, or attributes, **are not allowed** and will be removed by the catalogue web app.
-   **All links in it must be properly working.**
-   **It must include a hypertext link to the upstream repository** — where the font project files are made available (designer’s GitHub repository). You can copy the following line, and copy it at the bottom of the description file (don’t forget to adjust the URL):

``` code
To contribute, see <a href="https://github.com/owner/fontname">github.com/owner/fontname</a>
```

-   **Text should be updated when the font is upgraded** to let people know what changed.

    <span style="border-bottom:0.05em solid">Example:</span>

    > This font was upgraded in July 2021 to expand language coverage. It is now supporting Greek and Cyrillic.
-   **We only accept** **`.en_us`** **extension**, but you can definitely add a translation to the description in the case when the font is primarily targeting an audience reading a non-latin script.

See [Zen+Antique#about](https://fonts.google.com/specimen/Zen+Antique#about) as an example, provided by this file [DESCRIPTION.en_us.html](https://github.com/google/fonts/blob/main/ofl/zenantique/DESCRIPTION.en_us.html).

## Example

### Without localised text

See [Space+Grotesk#about](https://fonts.google.com/specimen/Space+Grotesk?query=Space+Grotesk#about) provided by [DESCRIPTION.en_us.html](https://github.com/floriankarsten/space-grotesk/blob/master/DESCRIPTION.en_us.html) as an example: it gives plenty of links (mini-website, original authors, referenced font published in GF), and follows all requirements.

**Html snippet**

``` code
<p>Space Grotesk is a proportional sans-serif typeface variant based on <a href="https://www.colophon-foundry.org">Colophon Foundry's</a> fixed-width <a href="https://fonts.google.com/specimen/Space+Mono">Space Mono</a> family (2016). 
Originally designed by <a href="https://fonts.floriankarsten.com">Florian Karsten</a> in 2018, Space Grotesk retains the monospace's idiosyncratic details while optimizing for improved readability at non-display sizes.</p>

<p><a href=https://floriankarsten.github.io/space-grotesk/><b>→ floriankarsten.github.io/space-grotesk</b><a><p>

<p>Space Grotesk includes Latin Vietnamese, Pinyin, and all Western, Central, and South-Eastern European language support, as well as several OpenType features (old-style and tabular figures, superscript and subscript numerals, fractions, stylistic alternates).</p>

<p>To contribute, see <a href="https://github.com/floriankarsten/space-grotesk" target="_blank">github.com/floriankarsten/space-grotesk</a>.</p>
```

**Result on Google Fonts**

> ***About Space Grotesk***
>
> *Space Grotesk is a proportional sans-serif typeface variant based on* [*Colophon Foundry*](https://www.colophon-foundry.org)*'s fixed-width* [*Space Mono*](https://fonts.google.com/specimen/Space+Mono) *family (2016). Originally designed by* [*Florian Karsten*](https://fonts.floriankarsten.com) *in 2018, Space Grotesk retains the monospace's idiosyncratic details while optimizing for improved readability at non-display sizes.*
>
> *[**→ floriankarsten.github.io/space-grotesk**](https://floriankarsten.github.io/space-grotesk)*
>
> *Space Grotesk includes Latin Vietnamese, Pinyin, and all Western, Central, and South-Eastern European language support, as well as several OpenType features (old-style and tabular figures, superscript and subscript numerals, fractions, stylistic alternates).*
>
> *To contribute, see [github.com/floriankarsten/space-grotesk](https://github.com/floriankarsten/space-grotesk).*

### With localised text

If the “first” script of your font is not Latin, we strongly recommend you to also provide a translation of the description using the actual main script. **This localised text must be in the same html snippet as the english text.**

See [Zen+Antique#about](https://fonts.google.com/specimen/Zen+Antique#about) as an example, provided by this file [DESCRIPTION.en_us.html](https://github.com/google/fonts/blob/main/ofl/zenantique/DESCRIPTION.en_us.html).

**Html snippet**

``` code
<p>Zen Antique features two kinds of Antique Japanese with Kanji.
The impression of the weights (thickness) of strokes are different among characters—Hiragana and Latin alphabets are slightly lighter, 
while Katakana and Kanji are slightly heavier, which gives the unique rhythm and taste in this font.
<a href="https://fonts.google.com/specimen/Zen+Antique+Soft">Zen Antique Soft</a> has a slightly rounded effect on the corners.</p>

<p>To contribute to the project, visit <a href="https://github.com/googlefonts/zen-antique">github.com/googlefonts/zen-antique</a></p>
<p>Zen Antique には、古風な雰囲気の二種類の漢字を含む日本語書体があります。
文字によって画線の太さに変化があり、ひらがなと欧文は細め、カタカナと漢字は太めで、フォントに独特のリズムと味わいを与えています。
また、<a href="https://fonts.google.com/specimen/Zen+Antique+Soft?subset=japanese">Zen Antique Soft</a> では、角が少し丸くなっています。</p>

<p>このプロジェクトに参加して貢献したい方は、次の URL をご参照ください。<a href="https://github.com/googlefonts/zen-antique">github.com/googlefonts/zen-antique</a></p>
```

**Result on Google Fonts**

> ***About Zen Antique***
>
> *Zen Antique features two kinds of Antique Japanese with Kanji. The impression of the weights (thickness) of strokes are different among characters—Hiragana and Latin alphabets are slightly lighter, while Katakana and Kanji are slightly heavier, which gives the unique rhythm and taste in this font. [Zen Antique Soft](https://fonts.google.com/specimen/Zen+Antique+Soft) has a slightly rounded effect on the corners.*
>
> *To contribute to the project, visit [github.com/googlefonts/zen-antique](https://github.com/googlefonts/zen-antique)*
>
> *Zen Antique* には、古風な雰囲気の二種類の漢字を含む日本語書体があります。 文字によって画線の太さに変化があり、ひらがなと欧文は細め、カタカナと漢字は太めで、フォントに独特のリズムと味わいを与えています。 また、*[Zen Antique Soft](https://fonts.google.com/specimen/Zen+Antique+Soft?subset=japanese)* では、角が少し丸くなっています。
>
> このプロジェクトに参加して貢献したい方は、次の URL をご参照ください。*[github.com/googlefonts/zen-antique](https://github.com/googlefonts/zen-antique)*
