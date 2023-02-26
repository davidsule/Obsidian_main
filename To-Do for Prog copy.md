Python assignment operator
Inheritance, subclasses
Namespaces, global/local cars
Numpy/scipy:  sparse / dense matrices 


Command line cursor navigation, deletion etc  
Symlink Dotfiles in version controlled (git) folder (bash, zsh, powerlevel10k, got config, sublime, etc and others?) Dotfile utilities: [https://dotfiles.github.io/utilities/](https://dotfiles.github.io/utilities/)  
list of bash/zsh packages installed  
sublime git integration  
Sublime Tutorial and navigation/ deletion etc  
GitHub tutorial  
Pycharm tutorial  
How does Anaconda / sublime / pycharm / bash (zsh) / git work together?  
global gitingnore file? (see corresponding missing semester page)  
oh my bash?  
LEarn fucking powershell :(  
add anaconda prompt / anaconda powershell to windows terminal  
pyflakes for python typing check? or only myPy?  
'private' method in Python (not private but something starting with m...  
review tuple python  
class vs instance vs static method python  
variable scopes  
mangling python  
subclasses python  
bash: create shortcuts for future use (like a shortcut for an often used location)  
what's a local python module?  
how to have several .py files in a project and use them together?  
backup anaconda environments?  
look at principle of floats again  
figure out how conda with WSL, CS Code, Pycharm etc  
ZSH / Oh my ZSH  
Syntax highlighting and autocomplete in Bash / ZSH  
packages for Bash / ZSH (tldr, shellcheck, ripgrep, tree, broot, nnn/ncurses, autojump, fd, and others)  
Linting in Sublime, enhancements (Flake8) [https://realpython.com/setting-up-sublime-text-3-for-full-stack-python-development/](https://realpython.com/setting-up-sublime-text-3-for-full-stack-python-development/)  
Symlink Dotfiles in version controlled (git) folder (or utility)  
Terminal emulator? (GPU acceleration?)  
VS Code Interactive Playground  
where are anaconda environments stored? how to back up?  


Learn about JSON  
Timsort (and simple bubble sort)  
learn about garbage collection in Python  
proper 2FA  
google cloud or smth to execute stuff in the cloud  
real backup and automate backup from online sources  
hotkey remapping (capslock etc) (explore leaderkey - is that only VIM?)  
learn blind typing  
mozilla containers extension (like facebook etc)
how does salted hash work?  
Fstring instead of .format
Generators in python
Review lambda functions, list comprehension and generated version of list comprehension (generator expression) eg:
% >>> a = [1, 2, 3, 4]
% >>>b = (2*x for x in a)
% >>>b
% <generator object at 0x58760>
% >>> for i in b: print(b, end=' ')
% ...
% 2 4 6 8
% >>>
% >>> c = [1, 2, 3, 4]
% >>>d = [2*x for x in a]
% >>>d
% [2, 4, 6, 8]
% >>>
Syntax: for generator version of list comprehension
(expression for i in s if condition)
Meaning:
% for i in s:
%     if condition:
%         yield expression
Note: parens on generator expression can be dropped if used as a single function argument, eg: sum(x*x for x in s)

Zip, unzip in python
VsCode linting, static formatter, my problems with it
view objects python
printf (.format)
bitwise operators
learn about google colab jupyter notebook
conda with google colab [medium towards data science article](https://towardsdatascience.com/conda-google-colab-75f7c867a522)
connect google colab to local VScode and conda environment
'properties' mechanism in Python that makes providing access to instance variables safe and elegant in classes (that would be otherwise poor practice) - what about name mangling
How to write functions that work with numpy arrays?
How to add optional arguments to function? Default values?
Magic methods
Name mangling, methods, variables, inheritance etc one vs two leading underscores (double only if name conflicts with attributes need to be avoided in classes design to be subclassed). One leading underscores for non-public methods and instance variables. One underscore: not name mangling but internal use indicator. Single leading underscore attributes can be modified from outside easily (with assigning a new value to the name, underscore included. If underscore is not included in the assignment operation, it won't be assigned, although no error is thrown.) Name mangled - two leading underscores - cannot be modified from the outside easily - only with including the class name like redcar.__Car__colour = white
Class variables?
cell and line magic pythhon