## The vim way

* dot: The dot(.) command can be used to repeat last change
* C: c$(change to end)
* s: cl(replace current character and stay in insert)
* S: ^C(Change entire line)
* I: ^i go into insert mode at the start of the line
* A: $a go into insert mode at the end of the line
* o: A<CR> insert newline in bottom
* O: ko insert newline at top
* f{char}: find char in current line forwards
* F{char}: find char in current line backwards
* ;: Semicolon, f{char} again forward or F{char} again backward
* ,: Comma, f{char} again backward or F{char} again forward
* /{pattern}: Scan document for next match(n, N to navigate forward and backward)
* ?{pattern}: Scan document for previous match(n, N to navigate backward and forward)
* :s/target/replacement: Perform substitution(& for repeat, u or undo for reverse) works on current line only
* :%s/target/replacement/g: Perform substitution on entire file
* *: When your cursor is on word, press *(now you can press n and N to navigate to all instances of the word under cursor)
* #: works in same way as * above, but n and N go the opposite direction. * finds next match, # finds previous match

---
## Normal Mode

* u: Undo 
* db: delete from cursor starting position to beginning of the word.
* dw: delete from cursor starting position to end of the word.
* daw: delete an entire word
* <C-a>: increments a number
* <C-x>: decrements a number
* Operator + Motion = Action
* d{motion}: d is operator while motion could be l, aw, ap(an entire para) etc

### Vims operator modes
* c: Change
* d: delete
* y: yank
* g~: Swap Case
* gU: Make lowercase
* gu: Make uppercase
* ">" : Shift right(indent right)
* "<" : Shift left(indent left)
* =: Auto indent
* !: Filter motion lines through an external program

* Check Vim-commentary plugin(for example: \\ap allows you to comment an entire paragraph in single swoop)
* textobj-entire plugin: adds two new text objects ie and ae which act upon entire file. For example to autoindent entire file, we could do dd=G or simply with this plugin =ae. With both plugins, you could do \\ae which could comment entire file as well. Quite handy isn't it?

---
## Insert Mode

* <C-h>: Delete back one character(h is from hjkl)
* <C-w>: Delete back one word
* <C-u>: Delete back to start of line
* The above commands are not unique to vim. These can be apparently used in bash shell aka command line as well.
* esc or <C-[>: Will bring you back to normal mode from insert mode. Mostly use esc(mapped to caps lock)
* <C-r>": will paste text yanked while you are in insert mode. " is the unnamed register. You can use any other register as well
* <C-r>=: Allows you to math calculations in insert mode(could be useful I guess?)
* gi: go to last insert position

### Replace mode

* Overwrite existing text with replace mode: R to go into replace mode. Useful if you want to replace exact amount of text. That is change cat to bat(three letters to three letters etc)
* Virtual Replace mode: gR can be used to replace tab character(tab character will be considered as 8 spaces for example in this mode depending on tab stop of your ) etc
* r{char}: works only on a single character
* gr{char}: works only on a single character as well

---
## Visual Mode

* v: takes you into visual mode
* V: takes you into visual-line mode
* <C-v> or <C-q>: takes you into visual-block mode
* gv: reselect last visual selection
* o/O: in visual mode, this allows you to go to the other end of the visual selection(very useful)
* Change line to uppercase: has two ways of doing it. In Visual mode: v$U or in normal mode gU$. you can apply this for other motions(w,b etc). you can also use ~ or g~ to toggle case or gu(u in visual mode) to make lowercase
* Visual block(<C-q> or <C-v>) is quite useful to change rectangular blocks of text.

---
## The Command Line mode

* Colon(:) enters you into command line mode
* :[range]delete [x] -> Delete specified lines into register x
* :[range]yank [x] -> Yank specified lines into register x
* :[line]put [x] -> Put the text from register x after the specified line
* :[range]copy {address} -> Copy the specified lines to below the line specified by {address}
* :[range]move {address} -> Move the specified lines to below the line specified by {address}
* :[range]join -> Join the specified lines
* :[range]normal {commands} -> Execute Normal mode {commands} on each specified line
* :[range]substitute/{pattern}/{string}/[flags] -> Replace the occurrences of {pattern} with {string} on each specified line
* :[range]global/{pattern}/[cmd] -> Execute the ex command [cmd] on all specified lines where the {pattern} matches

* Line Numbers as An Address:
  * :1p or :1print will print 1st line
  * :3p will print 3rd line
  * :$ will move the cursor to last line
  * Example: :3d will quickly delete 3rd line. Without ex command, we would have to go to 3rd line and then press dd

* Range of Lines as address
  * :2,5p -> will print lines 2 through 5(inclusive)
  * It takes the form :{start},{end}
  * We can use . symbol to represent the current line. 
  * That is if we are on line 2, we can say :.,5p which will print lines 2 through 5(inclusive)
  * :%p -> will print all lines. % has a special meaning which stands for all lines in current file. This is equivalent to :1,$p
  * :%s/cat/bat -> This replaces the first occurrence of cat with bat on each line.

* Specify a range of lines by visual selection
  * After selecting lines in visual mode, press :. It will show up as '<,'> in your ex command
  * This is quite useful when we want to run a substitute command on only a subset of the file
  
* Specify a range of lines by patterns
  * :/<html>/,/<\/html>/p

* Modify an address using an offset
  * Suppose we wanted to run ex command on every line inside html tag block but not on the lines that contain the html tag itself?
  * :/<html>/+1,/<\/html>/-1p
  * It takes the form of :{address}+n -> If n is not given, it defaults to 1
  * Suppose we want to execute a command on some lines starting with current line?
  * :.,.+3p
  
#### Summary
The syntax for defining a range is very flexible. We can mix and match line numbers, marks and patterns, we can apply an offset to any of them. Some symbols are given below

* 1 : First line of the file
* $ : Last line of the file
* 0 : Virtual line above first line of the file
* . : Line where the cursor is placed 
* 'm: Line containing mark m
* '<: Start of the visual selection
* '>: End of visual selection
* % : The entire file (shorthand for :1,$)

#### Duplicate lines with :t command

* :[range]copy {address}
* :6copy. -> Make a copy of line 6 and put it below the current line
* :6t -> t is shortcut for copy command
* mnemonic is copy TO

* :6t. -> Copy line 6 to just below the current line
* :t6 -> Copy the current line to just below line 6(range is current line since its not given)
* :t. -> Duplicate the current line(yyp, yyp uses register while :t doesnt)
* :t$ -> Copy the current line to end of the file
* :'<,'>t0 -> Copy the visually selected lines to the start of the file

#### Move lines with :m command

* :[range]move {address}
* :m -> is the shortcut for move

* @: -> This repeats the last ex command(quite **handy**)

#### Run normal mode commands across a range

* We can use :normal to run normal mode command on a series of consecutive lines
* After selecting in visual mode, press : and then type normal and then type the command you want to run
* We can execute normal command on entire file as well like this -> :%normal A;
* % represents entire file. So we go the end of each line(A) and append ;
* Before executing the specified Normal mode command on each line , vim moves the cursor to the start of the line so we dont have to worry about where the cursor is positioned when we execute the command.
* :%normal i// -> can be used to comment out entire js file for example
* Instead of typing full word normal, you can type :norm itself
* You can also tab complete your commands while in ex mode 
* You can also hit up arrow or down arrow key while in ex mode to get previous commands that you ran. Instead of using arrow keys, you could also use <C-p> or <C-n>

#### Insert current word at the command prompt

* when in ex command mode, press <C-r><C-w>. This will copy the word under your cursor. This will save some time while using find/replace or substitute command
* <C-r><C-w> will select word, while <C-r><C-a> will select WORD

#### Command Line Window

* While in normal mode, press q: -> This will open cmd window. Here you can edit historical commands using full modal editing power of vim. You can close this by typing :q

#### Run commands in the shell

* :!ls will run ls in shell from within vim itself. Use of exclamation key is important
* :!ruby % -> will run ruby command against current file name. On vims command line, % stands for current file name
* :shell -> will start an interactive shell in vim. Exit command kills the shell and returns you back to vim

* :shell -> Start shell (return to vim by typing exit)
* :!cmd -> Execute {cmd} with the shell
* :read !{cmd} -> Execute {cmd} in the shell and insert its stdout below the cursor
* :[range]write!{cmd} -> Execute {cmd} in the shell with [range] lines as stdin
* :[range]!filter -> Filter the specified [range] through external program {filter}

## Navigate Inside Files with Motions