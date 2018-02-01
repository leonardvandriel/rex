<img src="icon.jpg" alt="rex Icon" width="72"/>

# rex

*code here, run there.*

A simple utility to develop code locally, but test and run in remotely. By prefixing your command with rex, your application will be built and run remotely. Output is echoed right back and the folder tree is synced before and after. As seemless as it gets.

# Install

    ./bin/rex --install

Add `.rex/` to your (global) `.gitignore`.

# Configure

First create a config file that specifes the remote ip address and folder names:

    rex --init config

# Execute

You can now execute commands remotely. Some easy ways to verify this:

    rex ls
    rex pwd
    rex echo $USER

Now use rex while coding:

    rex make
    rex ./bin/myapp
    open data/output.jpg

For more info, run:

    rex --help
