<img src="icon.jpg" alt="rex Icon" width="72"/>

# Rex

*code here, run there.*

A simple utility to develop code locally and run it remotely. Just prefix your command with `rex`. Output is echoed right back and the folder tree is synced before and after. As seemless as it gets.


## Install

First install Rex in `/usr/local/bin`:

    ./src/main --install

Add `.rex/` to your (global) `.gitignore`.


## Configure

Create a config file that specifes the remote ip address and folder names:

    rex --init config

* `user`: the user to authenticate
* `addr`: host name, e.g. `192.168.0.10`
* `port`: port number to connect to, e.g. `22`
* `path`: relative path on remote, e.g.  `projects/mything`
* `push`: folder to sync before running the command, e.g. `input:data`
* `pull`: folder to sync after running the command, e.g. `output:logs`
* `ignore`: list of files and folders to exclude, e.g. `.*:/bin:/tmp`
* `prerun`: a command to execute before, e.g. `"source ~/.bashrc"`

WARNING: *Rex overwrites all remote files and folders on every run. Make sure to __backup all important data__ on the remote before continuing.*

A slight exception to this is the push and pull folder, for which Rex will overwrite files, but not delete any files or folders.

## Run remotely

*Did you backup your remote code and data?*

Now we can execute commands remotely:

    rex <any shell command>

A good start is to add `--dry` to prevent actual changes on the remote:

    rex --dry ls

This will list the files that will be changed and the command to be executed:

    <f.st.... file.txt
    .d..t.... src/system
    cd projects/mything; ls

A dryn run is usually a good start; it could inform additional changes to the config file, like adding to `ignore`.

To verify the commands are are actually run remotely, try:

    rex pwd
    rex lsb_release -a

Rex is most useful when developing code locally and running it on the remote host:

    rex make
    rex ./bin/myapp
    open data/output.jpg

There are some caveats, for example when you use logic and pipes. Fix by adding quotes or backslash:

    rex ls '|'' wc
    rex ls '&&' pwd
    rex ls \> list
    rex ls \; ls -l

To get more verbose output:

    rex --verbose ls
    rex --debug ls


## More options

To just push your local files to the remote, without running any command:

    rex --push

And to only pull from the remote:

    rex --pull

To run without any file syncing:

    rex --run ls

To inspect the current configuration:

    rex --current

To list all configurations:

    rex --list

To select another configuration:

    rex --select config2

For more info:

    rex --help


## Test

All tests can be run with `./test/test`.
