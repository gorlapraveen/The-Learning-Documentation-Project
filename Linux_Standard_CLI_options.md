# Linux Standard Command-Line Options : GNU Compatible

Over time, there has evolved a loose standard for the meanings of command-line option flags. The GNU utilities conform more closely to this "standard" than older UNIX utilities.

Traditionally, UNIX command-line options consist of a dash, followed by one or more lowercase letters. The GNU utilities added a double-dash, followed by a complete word or compound word.

The two most widely-accepted options are:

    -h

    --help

    Help: Give usage message and exit.

    -v

    --version

    Version: Show program version and exit.

Other common options are:

    -a

    --all

    All: show all information or operate on all arguments.

    -l

    --list

    List: list files or arguments without taking other action.

    -o

    Output filename

    -q

    --quiet

    Quiet: suppress stdout.

    -r

    -R

    --recursive

    Recursive: Operate recursively (down directory tree).

    -v

    --verbose

    Verbose: output additional information to stdout or stderr.

    -z

    --compress

    Compress: apply compression (usually gzip).

However:

    In tar and gawk:

    -f

    --file

    File: filename follows.

    In cp, mv, rm:

    -f

    --force

    Force: force overwrite of target file(s).


A complete table of recommended options for the GNU utilities is available [HERE](/GNU_coding_standards.pdf)

