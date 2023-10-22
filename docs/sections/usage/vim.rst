Learning Vim
==============

Vim is a powerful and efficient text editor. This guide will help you get started with its basics.

.. contents:: Table of Contents
   :local:

Modes
-----

Vim operates in various modes, the two most fundamental ones are:

- **Normal mode**: Navigate and manipulate text.
- **Insert mode**: Insert text.

Commands:
- ``i``: Enter **insert** mode (before the cursor).
- ``I``: Enter insert mode at the beginning of the line.
- ``a``: Enter **append** mode (after the cursor).
- ``A``: Enter append mode at the end of the line.
- ``o``: Open a new line below and enter insert mode.
- ``O``: Open a new line above and enter insert mode.
- ``ESC``: Return to normal mode from any other mode.

Movement
--------

In normal mode:
- ``h``: Move left
- ``j``: Move down
- ``k``: Move up
- ``l``: Move right

Faster Movement
---------------

- ``w``: Jump forwards to the start of a word.
- ``e``: Jump forwards to the end of a word.
- ``b``: Jump backwards to the start of a word.
- ``0``: Start of the line.
- ``$``: End of the line.
- ``G``: Go to the end of the file.
- ``gg``: Go to the beginning of the file.
- ``ctrl + u``: Move up half a screen.
- ``ctrl + d``: Move down half a screen.

Basic Editing
-------------

- ``x``: Delete a character (under the cursor).
- ``dw``: Delete a word.
- ``dd``: Delete a line.
- ``u``: Undo.
- ``ctrl + r``: Redo.
- ``yy``: Yank (copy) a line.
- ``p``: Paste below the cursor.
- ``P``: Paste above the cursor.

Searching
---------

- ``/[search-term]``: Search forward.
- ``?[search-term]``: Search backward.
- ``n``: Find the next instance of the search term.
- ``N``: Find the previous instance.

Save & Exit
-----------

- ``:w``: Write (save) changes.
- ``:q``: Quit (will complain if there are unsaved changes).
- ``:wq``: Write and quit.
- ``:x``: Same as ``:wq``.
- ``ZZ``: (Shift + zz) Same as ``:wq``.
- ``:q!``: Quit without saving.

Configurations
--------------

To customize Vim, you can create or edit the ``.vimrc`` file in your home directory. Here, you can set options, define keyboard shortcuts, or include plugins to extend Vim's functionality.

Suggestions for Practicing
--------------------------

1. **Vim Tutor**: Access the Vim Tutor by typing ``vimtutor`` in your terminal. This is a 30-minute interactive tutorial introducing the basics of Vim.
2. **Use Vim Daily**: Practice makes perfect. Edit text files, write code, or take notes in Vim.
3. **Configurations & Plugins**: Customize Vim to your needs. Explore the vast ecosystem of plugins to expand Vim's capabilities.

Happy Vimming!

