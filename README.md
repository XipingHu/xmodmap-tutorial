# xmodmap-tutorial

## Backup your key mapping and modifier keys
run
`xmodmap -pke > ~/Xmodmap/Xmodmap-origin`
to backup keycodes

run
`xmodmap -pm > ~/Xmodmap/Xmodmap-modifiers`
to backup modifiers

## Capture the keycode of pressed key
run
`xev`

For instance, when I pressed `Left Control`, these appeared in the terminal

```
KeyPress event, serial 41, synthetic NO, window 0x7e00001,
    root 0x188, subw 0x0, time 52364911, (-426,498), root:(538,527),
    state 0x0, keycode 37 (keysym 0xffeb, Control_L), same_screen YES,
    XLookupString gives 0 bytes: 
    XmbLookupString gives 0 bytes: 
    XFilterEvent returns: False

KeyRelease event, serial 41, synthetic NO, window 0x7e00001,
    root 0x188, subw 0x0, time 52365031, (-426,498), root:(538,527),
    state 0x40, keycode 37 (keysym 0xffeb, Control_L), same_screen YES,
    XLookupString gives 0 bytes: 
    XFilterEvent returns: False

```
Which indicates that the keycode of my `Left Control` is `37` and the name of `Left Control` in Xmodmap is `Control_L`

When I press `Left Win`
```
eyPress event, serial 40, synthetic NO, window 0x7a00001,
    root 0x188, subw 0x0, time 53147218, (-464,771), root:(500,800),
    state 0x0, keycode 133 (keysym 0xffe3, Super_L), same_screen YES,
    XLookupString gives 0 bytes: 
    XmbLookupString gives 0 bytes: 
    XFilterEvent returns: False

KeyRelease event, serial 40, synthetic NO, window 0x7a00001,
    root 0x188, subw 0x0, time 53147372, (-464,771), root:(500,800),
    state 0x4, keycode 133 (keysym 0xffe3, Super_L), same_screen YES,
    XLookupString gives 0 bytes: 
    XFilterEvent returns: False

```
Which indicates that the keycode of my `Left Win` is `133` and the name of `Left Win` in Xmodmap is `Super_L`

## Writing scripts

### Reassigning Control_L to Super_L
As we have known before, the keycode of my `Control_L` is 37. We now change it to `Super_L`
```
keycode 37 = Super_L
```

Then put it into `~/.Xmodmap`

### Resetting Modifiers
Since the Modifiers is associated with keycodes instead of keynames, you need to reset them.

Just add the following code at the end of `~/.Xmodmap`
```
clear shift
clear lock
clear control
clear mod1
clear mod2
clear mod3
clear mod4
clear mod5
add shift = Shift_L Shift_R
add lock = Caps_Lock
add control = Control_L Control_R
add mod1 = Alt_L Alt_R
add mod2 = Num_Lock
add mod4 = Super_L Super_R Hyper_L
add mod5 = ISO_Level3_Shift Mode_switch
```

## Applying Changes

Changes will automatically apply whenever you login.

You can also start it manually with
```
xmodmap ~/.Xmodmap
```
