# General compile script 
Compile, run and clear programs in different languages with a single command.<br> 
Currently C, C++, Java, Python, Rust, Go, latex and shell scripts are supported. <br>
The scripts are written in POSIX shell so they can be easily extended to add more languages. 

## Why
The idea for this script initially came when I was compiling and running C and C++ programs and wanted to have it done in a single command rather than 2 separate commands. Initially I just aliased the required commands to ```c```. Then I wanted the command to clear out the binaries and other unecessary intermediate files generated during compilation(I'm looking at you Java), so I turned it into a script.

Yes, I am aware that these just save me a couple of keystrokes but I was bored one evening and thought I'd do the typical Linux user thing of spending 6 hours to automate something that takes you 6 seconds. And over thousands of compilations and clears it's saved me a good amount of time.

## Using the ```c``` compilation script
For just the compilation script, add the ```c``` file from this repo, somewhere on your PATH. Then you can run ```c filename``` to compile any script in a supported language.
Convenience scripts for compiling(and cleaning) multiple different languages

## Using ```buildSystem```
On it's own buildSystem isn't very useful, essentially runs ```c``` and  requests input before exiting, but this behaviour allows it to run as a pop up. This is especially useful in text editors like vim and sublime where there isn't a very convenient way to run programs. Download buildSystem and add it somewhere on your PATH

### To use ```buildSystem``` in sublime:
Add a new build system with the following in it's .sublime-build file
```{
	"shell_cmd": "st -e buildSystem '$file'"
}
```
Now whenever you press Ctrl+B your code will run in a pop up and close after requesting input


### To use ```buildSystem``` in vim:
Add the follwing to your vimrc:
```
augroup runners
	autocmd!
	autocmd FileType sh map <buffer> <leader>r :w<CR>:exec '!' shellescape(@%, 1)<CR>
	autocmd FileType python map <buffer> <leader>r :w<CR>:exec '!st -e buildSystem' shellescape(@%, 1)<CR>
	autocmd FileType go map <buffer> <leader>r :w<CR>:exec '!st -e buildSystem' shellescape(@%, 1)<CR>
	autocmd FileType rust map <buffer> <leader>r :w<CR>:exec '!st -e buildSystem' shellescape(@%, 1)<CR>
	autocmd FileType c map <buffer> <leader>r :w<CR>:exec '!st -e buildSystem' shellescape(@%, 1)<CR>
	autocmd FileType cpp map <buffer> <leader>r :w<CR>:exec '!st -e buildSystem' shellescape(@%, 1)<CR>
augroup END

```
This maps <leader>r to the buildSystem. You can change this to whatever hot key you prefer

## Requirements:
Each language has its own requirements to use it with this script but these can easily be changed in the source code.
The only notable requirements are:
To compile C,C++: Make
To compile latex: latexmk
