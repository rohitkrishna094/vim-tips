# vim-tips
This is a personal repo of vim shortcuts and tips so I don't forget them

* I: Insert at start of the line
* A: Insert at end of the line(completely)
* ggyG: Copy entire file contents
* ggdG: delete entire file contents
* b: go to beginning of the previous word
* w: go to beginning of the next word
* ge: go to end of previous word
* e: go to end of the next word
* dd: delete entire line
* D: delete until end of line from current cursor position
* fP: find next P on current line and put cursor on P
* tP: find next P on current line and put cursor just before P(read as till P)
* fP: find previous P on current line and put cursor on P
* tP: find previous P on current line and put cursor just after P(read as till P)
* dfP: deletes everything till P including P
* dtP: deletes everything till P excluding P
* ciw: change inside word
* ci": change inside quotes
* cit: change inside tag(html or xml tag)
* ci(: change inside (
* ci{: change inside {
* yy: yank current line(copy line)
* p: paste after
* P: paste before
* o: add new line after current line
* O: add new line before current line
* 0: go to start of line(completely)
* $: go to end of line(completely)
* ^: go to start of line(non-space)
* g_: go to end of line(non-space)
* %: go to next bracket or come back 
* H: move the cursor to top
* M: move the cursor to the middle
* L: move the cursor to the bottom
* zt: move the view to the top
* zz: move the view to the middle
* z.: move the view to the middle but put cursor at first character(non-white)
* zb: move the view to the bottom
* :50 or 50gg or 50G: go to line 50
* ctrl+e: scroll down
* ctrl+y: scroll up
* ctrl+d: move screen down by half
* ctrl+u: move screen up by half
* ctrl+d: move screen downward/down by 1 full page
* ctrl+b: move screen backward/up by 1 full page
* *: find next word under current cursor. it highlights all such occurrences. Use n to find next, N to find previous
* #: opposite of *. find previous word under current cursor. Use n to find previous, N to find next.
* gi: It puts you in insert mode at the place where you **last** inserted text.
* ctrl+o: jump back similar to intellij's alt+ctrl+leftarrow
* ctrl+i: jump forward similar to intellij's alt+ctrl+rightarrow
* [{: jump to opening brace in {} block
* ]}: jump to closing brace in {} block
* [(: jump to opening bracket in () block
* ]): jump to closing bracket in () block
* [m: jump to starting of previous method in java like language
* ]m: jump to starting of next method in java like language
* [M: jump to ending of previous method in java like language
* ]M: jump to ending of next method in java like language

[(, ])  - same for ( ) block
[#, ]# - jump to prev / next #ifdef, #else, #endif
[* or [/, ]* or ]/ - jump to beginning / end of a C-style comment /*  */ 
[m, ]m, [M, ]M - jump to begining / end of a next / previous C++/Java... method
small word vs big WORD
-----------------------
* A word is always delimited by a space
* A word is delimited by non-keyword characters, which are configurable. Whitespace characters aren't keywords, and usually other characters (like ()[],-) aren't, neither. 
  Therefore, a word usually is smaller than a WORD; the word-navigation is more fine-grained.

marks
-----
* you can set bookmarks and come back to it.
* mm sets a mark at current position on register m. 
    - Press `m to go to that mark from anywhere.
    - Press 'm to go to that mark but put cursor on first character.
* Use Mm to set a mark so that you can go to any file from any other file.
* :marks : to view all existing marks
