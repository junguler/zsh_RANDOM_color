### zsh_prompt_with_random_colors
if you spend a lot of time in the terminal you'll know how boring it gets looking at that same prompt over and over again so lets add some variety to how it looks

### before you start
make sure to install ohmyzsh before doing anything, it makes some changes to how zsh works and improves your experience vastly

lets also comment out the line about the prompt because we are making our own

``` 
# ZSH_THEME="robbyrussell"
```

### my color pallete

| number | hex | image | number | hex | image |
|---|---|---|---|---|---|
| 0 | #1e1e1e | ![](stuff/0.png) | 8 | #777777 | ![](stuff/8.png) |
| 1 | #fe0094 | ![](stuff/1.png) | 9 | #fe0094 | ![](stuff/9.png) |
| 2 | #82b414 | ![](stuff/2.png) | 10 | #82b414 | ![](stuff/10.png) |
| 3 | #FD971F | ![](stuff/3.png) | 11 | #FD971F | ![](stuff/11.png) |
| 4 | #459ee0 | ![](stuff/4.png) | 12 | #459ee0 | ![](stuff/12.png) |
| 5 | #A376FE | ![](stuff/5.png) | 13 | #A376FE | ![](stuff/13.png) |
| 6 | #00c2f5 | ![](stuff/6.png) | 14 | #00c2f5 | ![](stuff/14.png) |
| 7 | #b9b9b9 | ![](stuff/7.png) | 15 | #b9b9b9 | ![](stuff/15.png) | 

### how?
as you probably know `%F{}` is to set colors in your prompt, `%f` will reset the color to normal, what you do is sandwich a section or the whole of your prompt that you want to apply color between these 2, something like this for example

```
PROMPT='%F{1}junguler%F{2}@%F{3}nowhere%f  '
```

![](stuff/1-1.png)

using that same pattern we can use the built in '$RANDOM' variable to set a random color for each time you press inter or use a command in your shell

```
PROMPT='%F{$(($RANDOM%6+1))}junguler%F{$(($RANDOM%6+1))}@%F{$(($RANDOM%6+1))}nowhere%f '
```

this will apply a random color between 1 and 6 each time, which will result in one of the following colors: red, green, yellow, blue, magenta or cyan

![](stuff/1-2.png)

now that you know how easy it is to get things going you can apply the same method to all of the items in your prompt, note that you don't need to reset the color each time if the next item is also going to get it's own color, just at the end of your prompt or when you want a section of your prompt to be the default color

here as example of my own prompt including time, current working directory and the status code of the last command that ran

```
PROMPT='%F{$(($RANDOM%6+1))}%D{%H:%M} % %F{$(($RANDOM%6+1))}%1~ %F{$(($RANDOM%6+1))}%?%f '
```

![](stuff/1-3.png)

looks cool but it's a little empty, so lets add some square brackets to make it look better and also give us a few more things to randomly color

```
PROMPT='%F{$(($RANDOM%6+1))}[%F{$(($RANDOM%6+1))}%D{%H:%M}%F{$(($RANDOM%6+1))}] %F{$(($RANDOM%6+1))}[%F{$(($RANDOM%6+1))}%1~%F{$(($RANDOM%6+1))}] %F{$(($RANDOM%6+1))}[%F{$(($RANDOM%6+1))}%?%F{$(($RANDOM%6+1))}]%f '
```

![](stuff/1-4.png)

### what about 256 colors

the same method also applies with 256 colors, just adjust the RANDOM numbers to `$((RANDOM%215+16))`, note that many of these colors have poor contrast against each other and possibly the background color of you terminal emulator 

![](stuff/256.png)

you can't usually change how the colors 16-255 look unless you are on a terminal emulator that supports filters or css, what you see is what you get pretty much

```
PROMPT='%F{$((RANDOM%215+16))}[%F{$((RANDOM%215+16))}%D{%H:%M}%F{$((RANDOM%215+16))}] %F{$((RANDOM%215+16))}[%F{$((RANDOM%215+16))}%1~%F{$((RANDOM%215+16))}] %F{$((RANDOM%215+16))}[%F{$((RANDOM%215+16))}%?%F{$((RANDOM%215+16))}]%f '
```

![](stuff/2-1.png)

### more control using ranges of colors
too much randomness leads to ugly results as you can see from the above picture, so lets use ranges of colors to better control our prompts while still having the option of variety of colors to choose from

lets look at the 6 color blocks that include the colors of 256-xterm color pallete

| ![](stuff/16-51.png) | ![](stuff/52-87.png) | ![](stuff/88-123.png) |
|---|---|---|
| ![](stuff/124-159.png) | ![](stuff/160-195.png) | ![](stuff/196-231.png) |

as you can see there are quite a few good color combinations to choose from but not all of them are beside each other

the `$RANDOM` variable doesn't give you the option to choose from several ranges of colors but it does have the option of using simple math to exclude numbers we don't want so we can have a better range of colors, so lets show some examples to make this easy to understand

| direction | code | image | 
|---|---|---|
| top to bottom | `$((162+($RANDOM%6)*6))` | ![](stuff/down.png) |
| left to right | `$((160+($RANDOM%6)))` | ![](stuff/right.png) |
| top-left to bottom-right | `$((160+($RANDOM%6)*7))` | ![](stuff/backslash.png) |
| top-right to bottom-left | `$((163+($RANDOM%6)*5))` | ![](stuff/slash.png) |

as you can see it's quite easy to get a range of colors from each block of 6x6, just start with the number you want and apply it to the `$RANDOM` variable

### some interesting combinations to consider
having learned how it works lets make some color palletes to use for our random prompts

| theme | code | colors | image | 
|---|---|---|---|
| warm | `$((196+($RANDOM%6)*6))` | ![](stuff/196.png) ![](stuff/202.png) ![](stuff/208.png) ![](stuff/214.png) ![](stuff/220.png) ![](stuff/226.png) | ![](stuff/warm.png) |
| cold | `$((93+($RANDOM%6)*6))` | ![](stuff/93.png) ![](stuff/99.png) ![](stuff/105.png) ![](stuff/111.png) ![](stuff/117.png) ![](stuff/123.png) | ![](stuff/cold.png) |
| purple/green | `$((93+($RANDOM%6)*5))` | ![](stuff/93.png) ![](stuff/98.png) ![](stuff/103.png) ![](stuff/108.png) ![](stuff/113.png) ![](stuff/118.png) | ![](stuff/pur-to-gre.png) |
| pink/yellow | `$((201+($RANDOM%6)*5))` | ![](stuff/201.png) ![](stuff/206.png) ![](stuff/211.png) ![](stuff/216.png) ![](stuff/221.png) ![](stuff/226.png) | ![](stuff/pin-to-yel.png) |

### multi color pallete prompt
so far we decided on a color pallete and applied it to the whole of the prompt but because it's all modular it's really easy to have several color combinations at once

| code | colors | 
|---|---|
| $((RANDOM%6+46))
 | ![](stuff/46.png) ![](stuff/47.png) ![](stuff/48.png) ![](stuff/49.png) ![](stuff/50.png) ![](stuff/51.png) |
| $((57+($RANDOM%6)*6))
 | ![](stuff/57.png) ![](stuff/63.png) ![](stuff/69.png) ![](stuff/75.png) ![](stuff/81.png) ![](stuff/87.png) |
| $((93+($RANDOM%6)*6))
 | ![](stuff/93.png) ![](stuff/99.png) ![](stuff/105.png) ![](stuff/111.png) ![](stuff/117.png) ![](stuff/123.png) |
| $((129+($RANDOM%6)*5))
 | ![](stuff/129.png) ![](stuff/134.png) ![](stuff/139.png) ![](stuff/144.png) ![](stuff/149.png) ![](stuff/154.png) |
| $((RANDOM%6+196))
 | ![](stuff/196.png) ![](stuff/197.png) ![](stuff/198.png) ![](stuff/199.png) ![](stuff/200.png) ![](stuff/201.png) |
| $((196+($RANDOM%6)*6))
 | ![](stuff/196.png) ![](stuff/202.png) ![](stuff/208.png) ![](stuff/214.png) ![](stuff/220.png) ![](stuff/226.png) |
| $((201+($RANDOM%6)*5))
 | ![](stuff/201.png) ![](stuff/206.png) ![](stuff/211.png) ![](stuff/216.png) ![](stuff/221.png) ![](stuff/226.png) |


```
PROMPT='%F{$(($RANDOM%6+46))}[%F{$(($RANDOM%6+46))}%D{%H:%M}%F{$(($RANDOM%6+46))}] %F{$(($RANDOM%6+196))}[%F{$(($RANDOM%6+196))}%1~%F{$(($RANDOM%6+196))}] %F{$((201+($RANDOM%6)*5))}[%F{$((201+($RANDOM%6)*5))}%?%F{$((201+($RANDOM%6)*5))}]%f '
```

![](stuff/.png)

### background colors
using the same methods we learned it's easy to apply a background color to your prompt using `$K{}` and `$k`

![](stuff/232-255.png)

```
$(($RANDOM%7+232))
```

which uses color numbers between 232 to 238

![](stuff/background.png)

just make sure to keep the contrast level enough to have the prompt easily readable

### add variables
the code works but it's too complicated to change, so lets add a few variables to `.zshrc` to make life easier

```
local l_l='['
local r_r=']'
local s_s=' '
local _01='$(($RANDOM%6+1))'
```

so lets unpack this, `l_l='['` is the left braket, `local r_r=']'` the right bracket, `local s_s=' '` the white space between the prompt sections and `_01='$(($RANDOM%6+1))'` is the first instance of our random color

the random color variable is only good for one time in the prompt so we need to make a new one for every time we need a random color

you can use these variables in your prompt by simply adding a dollar sign `$` behind them like this `$_01`

so lets tidy up that prompt from the above example and make it way more usable, lets also add more color variables to the `.zshrc` make sure to place them above the prompt

```
local l_l='['
local r_r=']'
local s_s=' '
local _01='$(($RANDOM%6+1))'
local _02='$(($RANDOM%6+1))'
local _03='$(($RANDOM%6+1))'
local _04='$(($RANDOM%6+1))'
local _05='$(($RANDOM%6+1))'
local _06='$(($RANDOM%6+1))'
local _07='$(($RANDOM%6+1))'
local _08='$(($RANDOM%6+1))'
local _09='$(($RANDOM%6+1))'
```

```
PROMPT='%F{$(($_01))}${l_l}%F{$(($_02))}%D{%H:%M}%F{$(($_03))}${r_r}${s_s}%F{$(($_04))}${l_l}%F{$(($_05))}%1~%F{$(($_06))}${r_r}${s_s}%F{$(($_07))}${l_l}%F{$(($_08))}%?%F{$(($_09))}${r_r}%f '
```

the other benefit of having a variable in your prompt is you can just as easily change everything about those variables and have it automatically take effect in the prompt, so lets show and example of this

say i don't want to have square brakets in my prompt, lets change them to parentheses like this ``local l_l='('`` ``local l_l=')'``

same thing applies for your color variables