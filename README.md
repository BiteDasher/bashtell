# bashtell
An engine for creating short stories written in bash

## Possible output characteristics
Total possible values for strings: 4 \
Possible values:
- `*` - Text output.  Most often used to display multiple lines.
- `+` - The text that will be displayed before the selection
- `?` - Selection options
- `/` - Ending

## Game file structure
`characteristic` `step number`-`depend step`-`dependent answer`

Example: `*1-0-0 Something`

Larger example:
```
0-This is start
*1-0-0 First (*) message
*1-0-0 Second (*) message##With beautiful tab
*1-0-0 @@3 Third (*) message with 3 seconds timeout @@
+2-1-0 This is the (+) message before the choice
?3-2-1 Option 1
?3-2-2 Option 2
?3-2-3 Option 3
+4-3-1 Chosed Option 1
*5-4-1 Simple text
*5-4-0 Simple text (2)
/6-5-0 End of Option 1
+7-3-2 Chosed Option 2
*8-7-2 Simple text(2)
/9-8-0 End of Option 2
*10-3-3 Long long long message of Option 3
+11-10-0 This is the second choice of the message.
?12-11-1 Option 1 of the second message
?12-11-2 Option 2 of the second message
/13-12-1 End of Option 1 of the second message
/13-12-2 End of Option 2 of the second message
```

## Gameplay example:
```
This is start

< First (*) message
  With beautiful tab
< Second (*) message
< Third (*) message with 3 seconds timeout @@

<... This is the (+) message before the choice
1: Option 1
2: Option 2
3: Option 3
> 3

< Long long long message of Option 3

<... This is the second choice of the message.
1: Option 1 of the second message
2: Option 2 of the second message
> 1

<=== End of Option 1 of the second message
```

## Tips:
- After answering the question (`?`) When using the message (`*`), the previous dependent step is reset
```
?3-2-1 1
?3-2-2 2
*4-3-1 1 was chosen
*4-3-0 ...
```
- Before using answer options (`?`), It is strictly necessary to use `+`
- You can set a timeout before the output message using `@@time ` (doesn't work in `?`)
- You can save the current progress and load it. To save, just press `Ctrl + C`
- To load progress, type `-l` or `--load` after the name of the game file
- Use `##` symbols (as in the example) to form neat lines in the text (it helps if you need more than one line in one message)
- The transition to a new line is carried out after: the last message with `*` and after answering the question (`?`)

## Needed binaries:
```
bash
base64
grep
tail
tr
```
