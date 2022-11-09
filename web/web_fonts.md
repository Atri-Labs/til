# What are web fonts?

Web fonts, a.k.a icon fonts, works by using a font file (.ttf etc.) and CSS file under the hood. The font file, like any other normal font file, contains glyphs for support unicode characters. The CSS file, such as provided by Font Awesome, have little tricks inside them to make the web fonts easy to use just by using classes. The trick is to use a `class` with `after` or `before` pseudo elements to insert the unicode as content and font details.

More details on the implementation is well explained here `https://webstandardssherpa.com/reviews/responsive-webfont-icons`.

Recently a new kind of fonts have been introduced called SVG fonts that have certain advantages/disadvantages over web fonts. A detailed study can be found in the Font Awesome website.

# How to use web fonts?

You can import that CSS file like you import a normal CSS file. The CSS file will contain a `@font-face` rule that will have link to the font file with glyphs.
