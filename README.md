GitResultsManager
=====================

Note: GitResultsManager does not profess to be remotely operable on
any operating system other than Linux and Mac. Evidence of success on
other OSs is appreciated.



Installing
---------------------

### One line install:

    git clone https://github.com/yosinski/GitResultsManager.git && \
    cd GitResultsManager && \
    sudo python setup.py install && \
    sudo cp gitresman gitresmantimediff grmtd git-recreate /usr/local/bin

Replace /usr/local/bin with another location on your path, if desired.



Usage
---------------------

GitResultsManager may be used in two ways:

1. Using the `gitresman` wrapper script to run programs in any language, or
2. From within Python as a Python module.

(1) is more general, while (2) offers more control. The following examples are available in the `examples` directory.

### Example of using `gitresman` wrapper script to run a C program:

First, we'll compile the `demo-c` program (from the examples directory) and run it without `gitresman`:

    g++ -o demo-c demo-c.cc   # compile program first if necessary
    ./demo-c

Output:

    Environment variable GIT_RESULTS_MANAGER_DIR is undefined. To demonstrate logging, run this instead as
        gitresman junk ./demo-c
    This line is logged
    This line is logged (stderr)
    This line is logged
    This line is logged (stderr)
    This line is logged
    This line is logged (stderr)

Notice that it complains it cannot find the GIT_RESULTS_MANAGER_DIR
environment variable. This is how the program knows it is not being
run from within `gitresman`. Now, running it within `gitresman`:

    gitresman run-name ./demo-c

Output:

    WARNING: GitResultsManager running in GIT_DISABLED mode: no git information saved! (Is /Users/jason/temp/examples in a git repo?)
      Logging directory: results/121030_183101_run-name
            Command run: ./demo-c
               Hostname: lapaz
      Working directory: /Users/jason/temp/examples
    The current GIT_RESULTS_MANAGER_DIR is: results/121030_183101_run-name
    This line is logged
    This line is logged
    This line is logged
    This line is logged (stderr)
    This line is logged (stderr)
    This line is logged (stderr)
           Wall time:  0.024
      Processor time:  0.012

Notice how `gitresman` adds a few lines of information to the beginning and ending of the output? Looking at each line in order:

    WARNING: GitResultsManager running in GIT_DISABLED mode: no git information saved! (Is /Users/jason/temp/examples in a git repo?)

Warning because we aren't running from within a git repoitory, removing most of the usefulness of GitResultsManager.

      Logging directory: results/121030_183101_run-name

The directory that was created for this run, in the format <datestamp>_<timestamp>_<name of run>

            Command run: ./demo-c

Which command you actually ran.

               Hostname: lapaz

The host this run was performed on (useful when running on clusters)

      Working directory: /Users/jason/temp/examples

The working directory. Next follows the acutual output of the program, and then at the end...

           Wall time:  0.024
      Processor time:  0.012

`gitresman` notes how long the program took to execute in wall time and processor time.



Developement task list
----------------------

### To do

1. Add settings override in ~/.config/gitresultsmanager_config.py
1. Documentation

Want to help? Fork and submit a pull request!
