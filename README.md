# mathmusic_macro

[![license](https://img.shields.io/github/license/george-chou/mathmusic_macro.svg)](https://github.com/george-chou/mathmusic_macro/blob/master/LICENSE)
[![CI](https://github.com/george-chou/mathmusic_macro/workflows/CI/badge.svg?branch=master)](https://github.com/george-chou/mathmusic_macro/actions)

A macro package for simplification of composition on Mathematica

## USER MANUAL

For tonal modifying operation, numbers are more convenient than note symbols in Mathematica. There is a one-to-one correspondence between notes and integers shown as the left form below.

<div align=center>
    <b>Table 1: Note scheme</b><br>
    <img width="500" src="https://george-chou.github.io/covers/mathmusic_macro/t1.png"/>
</div>

The 12-note scheme presents all the notes in a simple format that is unfriendly to us, while people are used to 7 letters from _C_ to _B_ once the tonality is specific. The key is to find a map from the 7-note scheme to the 12-note scheme to operate an inconvenient way.

We show inputting formats of different effects in the form below.

<div align=center><b>Table 2: Input formats</b><br></div>

| Effect | Format | Remark |
| --- | --- | --- |
| Rest | *{l}* | *l* is beat number; |
| Tone | *{n, l}* | *n* is note number; |
| Chord | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l}* | *n<sub>k</sub>* are note numbers of the chord; |
| Stagato | *{n, {l<sub>1</sub>, l<sub>2</sub>}}* | *l<sub>1</sub>* is beat number, *l<sub>2</sub>* is sound head's duration rate of total; |
| Vibrato | *{{n<sub>1</sub>, n<sub>2</sub>}, l<sub>1</sub>, l<sub>2</sub>}* | *l<sub>2</sub>* is trill number; |
| Mordent | *{{n<sub>1</sub>, n<sub>2</sub>, ...}, l<sub>1</sub>, l<sub>2</sub>}* | *l<sub>2</sub>* is step's duration rate of total; |
| Tenuto | *{bottom notes, {top notes}}* | Bottom notes can be single tones or chords, top notes can be any type mentioned above. |

With these rules, we can get a concise format of notes.

<div align=center>
    <b>Table 3: Simplified codes for effects</b><br>
    <img width="605" src="https://george-chou.github.io/covers/mathmusic_macro/t3.PNG"/>
</div>

We save those notes as vectors, let the computer estimate their types according to their inputting formats.

At this time, we can change this score paragraph into whichever tonality you want by replacing the first and the second variate in the function. And you can move the whole song up or down by altering the third variable. But this is still limited for those songs within parts in different tonalities. So, I tried to expend the song vector, let them hold not only one paragraph, and the information of each section was previously reserved. The new format of the song is like this:

```
song = {
    {info of paragraph 1},
    {paragraph 1},

    {info of paragraph 2},
    {paragraph 2},

    ...

    {info of paragraph n},
    {paragraph n},
};
```

The information includes the tonality of the section(major or minor and central note), the offset of section and speed, while the section itself contains notes. I took advantage of this occasion, added some new properties such as volume and volume gradient.

The volume linearly decreases with notes. The information part temporarily contains these properties, and its input format follows the rules below.

<div align=center><b>Table 4: Information formats</b><br></div>

| Format | Remark |
| --- | --- |
| *{m, c, s, t}* | *m* is 0(major) or 1(minor); *c* is central note integer([0, 11]); *s* is offset; *t* is beat number per minute; |
| *{m, c, s, t, v}* | *v* is volume; |
| *{m, c, s, t, {v<sub>s</sub>, v<sub>t</sub>}}* | *v<sub>s</sub>* is starting volume; *v<sub>t</sub>* is terminal volume. |

Please refer to the demo code _Demo_BWV-1079.nb_ for more details; Before compiling songs, please run the macro package first.
