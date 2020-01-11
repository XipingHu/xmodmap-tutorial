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

Then put it into `~/.Xmodmap`, it will apply when X starts.

Start it manually with
```
xmodmap ~/.Xmodmap
```
