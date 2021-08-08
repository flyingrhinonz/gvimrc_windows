For those hardcore linux engineers who can't adjust to notepad, vim still can be used on windows 10. It just takes a bit of setup.

Install gvim on your machine - choose the full install - this is very important because you'll miss out on intergrations and components if you choose the more minimal install options.
In the key mappings screen - you have choices between mapping the windows **ctrl <?>** keys in vim or not. Depending upon how easily you want to integrate with the rest of your windows environment you can choose different options. Remember though -  **ctrl v**  is visual block in vim, so if you're truly hardcore vim then choose not to remap and learn the alternatives.
I've chosen not to integrate windows keys into vim. vim key maps will behave normally.

Here's how to get text into/outof vim to windows clipboard:
- At the windows end:
 - Everything is normal and as you're used to with the **ctrl c/v/x**
- At the vim end:
 - If you're copying/cutting out of vim:
  - **ctrl insert** : to copy . Alternatively simply setup vim to copy upon select (that's what I've done).
   - For some HP laptops that are missing the INS key - it's **Fn E** [HP page](https://h30434.www3.hp.com/t5/Business-Notebooks/There-is-no-INSERT-key-on-the-new-2018-Hp-840-elitebook-G5/td-p/6695864)
  - **shift delete** : to cut
 - If you're pasting in to vim:
  - **shift insert** : to paste
 - Documented here: [vim wiki](https://vim.fandom.com/wiki/Copy,_cut_and_paste)
 - Alternatively, choose to remap the keys and put up with lost vim functionality, although **ctrl <?>** will now behave as in the rest of windows


gvim default settings are pretty rubbish - they look like a notepad page. Definitely edit the vimrc file (see tips section, or my example file) to make the most of vim.
Watch out for this line: **autocmd FileType text setlocal textwidth=78** in **c: / program files (x86) / vim / vim82 / vimrc_example.vim**
It causes text wrap and is really annoying. If I want to wrap text I will press ENTER myself, not have vim decide for me.
You can check it's status using:  **:verbose set tw?**
Displays the last instance of this value being set - so if you didn't modify it as per my config below, you'll see it as loaded in the default example above.
Once you override it per my example below - this setting will come into effect when a text file is loaded (not before).


Config files load order:

You'll notice that vim behaves strangely and not understand where these configs are coming from. Here's the order in which they are loaded:

c: / Program Files (x86) / vim / _vimrc
This then has a line that sources: source $VIMRUNTIME/vimrc_example.vim
Which results in  this file getting sourced:
c: / Program Files (x86) / vim / vim82 / vimrc_example.vim
Which in turn sources: source $VIMRUNTIME/defaults.vim
Which results in  this file getting sourced:
c: / Program Files (x86) / vim / vim82 / defaults.vim
These two files result in a lot of evil and unexpected behavior!
Finally, your own settings file is read (_gvimrc) - see below for details on this file
You'll need to undo a lot of default settings (by overwriting their values in _gvimrc - because the defaults are not helpful to users who want to be productive - after all - you're that's the reason you are using vim and not notepad!)
See my tips below


Tips:

Settings file (what we know as /etc/vim/vimrc in linux) is called c: / program files x86 / vim / _vimrc
Create a file called:   _gvimrc
And put your settings here.
This is your local file (equivalent to: /etc/vim/vimrc.local   in linux)
You can check your $HOME directory by typing into vim command mode:
:echo $HOME
And  the location you need to put your _gvimrc file (this is the one you'll use):
:echo $MYGVIMRC
Or your _vimrc file:
:echo $MYVIMRC
If you really can't ditch the command line and prefer pure vim (well as close as windows will allow) -
Windows key ? Power shell
'cd' to whatever directory you are working in
vim <filename>  - and you'll get a terminal vim
Start vim in the Win10 GUI with: gvim
Or vim/gvim from the cmd terminal
If you like persistent undo (can undo even if you close the file and open it again), see this:
  set undofile                 "turn on the feature
  set undodir=$HOME/.vim/undo  "directory where the undo files will be stored
I actually use this in my setup - the undofile setting comes from vim install, and the undodir is overwritten by me in my _gvimrc


