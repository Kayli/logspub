# notes about how to use vi editor

## basics

- has multiple modes
  - normal (default one)
    - 'esc' key to return to normal from any other mode
  - insert
    - function: edit text like you would in a normal editor
    - 'i' or 'a' key
  - command
    - ':' key
    - function: enter commands
  - visual
    - 'v' or 'V' key
    - function: text selection


## normal mode hotkeys

- remove current line                 dd
- paste                               p
- copy (yank)                         y
- move to next paragraph              }
- delete to next paragraph            d}
- start selection at cursor position  v 
- start selection by lines            V
- tab visual selection                < or >
- undo                                u
- redo                                r
- save and quit                       ZZ
- insert before cursor                i
- insert after cursor                 a
- search forward                      /string
- search backward                     ?string
- repeat search/inverse               n/N
- show current line number and file   ctrl+g 


## commands

- save current file     :w
- quit editor           :q
- save and quit         :wq
- enforce command       :q!
- open file             e <filename>
- open shell            :sh (ctrl+d to exit)


