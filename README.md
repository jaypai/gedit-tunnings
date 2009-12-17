gEdit Tunnings
==============

gEdit tunnings holds my personal setup to make the editor work my way. Anyone 
interested in using gEdit for VBScript, Javascript, Python, Ruby, MSSQL, C# and 
others may check this repository for small tips and tricks.

Enable Menu Shortcut keys
-------------------------

This is a great tip! GNOME let you to change the menu shortcuts really easily! 
Using Ubuntu, you should:

    Click System > Preferences > Appearance
    Click Interface tab
    Check "Enable menu shortcut keys"

After this, you can set any shortcut to any menu just focusing the menu option
and typing the keys you want to use as shortcut. To rollback, just use `backspace`.

External Tools
--------------

_Note:_ Please, if you fork and add a new external tool to this collection, keep
the sorting by the `H3` name.

### Diff

Pre-requisites:

    sudo apt-get install zenity meld

Description: **Diff the current document against another one**  
Shortcut Key: `<Control><Alt>d`  
Commands:  
    #!/bin/sh

    meld $GEDIT_CURRENT_DOCUMENT_DIR/$GEDIT_CURRENT_DOCUMENT_NAME `zenity --file-selection --title="External Tools - Diff against ..."` &
Input: **Nothing**  
Output: **Display in the bottom pane**  
Applicability: **Local files only**

### Format as HTML 4.01

Pre-requisites:

    sudo apt-get install tidy

Description: **Tidy to HTML 4.01**  
Shortcut Key:  
Commands:  
    #!/bin/sh

    exec tidy -utf8 -ashtml -wrap 0 -indent -upper -quiet "$GEDIT_CURRENT_DOCUMENT_NAME"
Input: **Nothing**  
Output: **Create new document**  
Applicability: **Local files only**

### Format as XHTML 1.0

Pre-requisites:

    sudo apt-get install tidy

Description: **Tidy to XHTML 1.0**  
Shortcut Key:  
Commands:  
    #!/bin/sh

    exec tidy -utf8 -asxhtml -wrap 0 -indent -quiet "$GEDIT_CURRENT_DOCUMENT_NAME"
Input: **Nothing**  
Output: **Create new document**  
Applicability: **Local files only**

### Format Javascript

Pre-requisites:

This tool requires [einars jsbeautifier](http://github.com/einars/js-beautify "jsbeautifier").
Just set `jsbeautify_path` in the `Commands` to the right place.

Description: **Beautify Javascript using einars jsbeautify**  
Shortcut Key:  
Commands:  
    #!/usr/bin/env python

    import os
    import sys
    import tempfile

    jsbeautify_path = "/home/nagaozen/Development/js-beautify/"

    content = sys.stdin.read()
    h, tmpfile = tempfile.mkstemp()
    os.close(h)

    f = open(tmpfile, "w")
    f.write(content)
    f.close()

    cmd = "java org.mozilla.javascript.tools.shell.Main beautify-cl.js -i 4 %s"%(tmpfile)
    os.chdir(jsbeautify_path)
    content = os.system(cmd)
    os.remove(tmpfile)

    print content
Input: **Current Selection**  
Output: **Replace the current selection**  
Applicability: **All documents**

### Hyphenate

Description: **Hyphenates a sentence**  
Shortcut Key: `<Control><Alt>h`  
Commands:  
    #!/usr/bin/env python

    import sys

    print sys.stdin.read().replace(" ", "-").lower()
Input: **Current Selection**  
Output: **Replace the current selection**  
Applicability: **All documents**

### Parse a LESS document

Pre-requisites:

    sudo apt-get install ruby rubygems
    sudo gem install less

Description: **LESSC the current document**  
Shortcut Key:  
Commands:  
    #!/usr/bin/env ruby

    require 'rubygems'
    require 'less'

    puts Less.parse($stdin.read)
Input: **Current Document**  
Output: **Create new document**  
Applicability: **All documents**
