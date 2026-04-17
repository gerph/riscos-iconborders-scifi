I want to make some SciFi style buttons instead of the drab buttons we currently
have.
The code here is a RISC OS module and a command line tool that will test how the
buttons look. The actual button borders are drawn in c/borders.
To build the code that draws the buttons we use `riscos-amu -f MakefileApp`.
To test that the code is working, we use: `riscos-build-run aif32 --command 'aif32.IconBorderSciFi -save-native' --return-file Screen --return-to Screen.png`

Colours are in RISC OS format &BBGGRR00.

The button drawing has a number of stages:

* The `border_state` function is called to ask whether the button is highlightable (changes when you float over it) `STATE_HIGHLIGHTABLE`; and whether the whole button needs a redraw because it changes shape when you click or float over it) `STATE_CHANGESSHAPE`
* The `border_colour` function is told what colours are to be used (and can override the colours by updating the values).
* The border background is drawn with `border_fill()`. This the content that sits behind the text.
* The `border_size` call is called (outside this code) and the size of the box returned is where the text is allowed to be drawn. The text is then drawn (outside this code) within that box.
* The border outline is then drawn with border_draw().

Flags are passed to the border functions to indicate the state of the icon.
Flag 21 (1<<21) indicates that the button is pressed.
Flag 23 (1<<23) indicates that the button is being floated over.

The button types we are interested in are the button types 5 and 6.

I'd like the buttons to have something of the style of https://img.freepik.com/premium-vector/web-buttons-set-technology_984207-363.jpg.

I like the blue/neon-cyan style. Try to keep to this, but allow the background/highlight colours to be configurable at runtime.

Button type 4 should be more plain, as the regular button.

Button type 5 should be more pretty, as this is the 'default' button.

Please look at the styled images and then decide what sort of image you want for the two buttons.

I would like the work done in sections, pausing between each to check whether things look right or not.

1. Get the two buttons drawn plain (don't worry about the highlighting or the selected state).
2. Create a selected form of the button which presses or shows somehow that it would activate.
3. Create a highlighted form which shows the button in a 'this would do something if you clicked it' state.

Ask me any questions up front if you want to check anything.
Commit your code when you're feeling that things have improved.
