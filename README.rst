What this is
============

A place for testing released `distlib` launchers.

The actions in this repo make and run executable launchers using the launchers from the
most recent release of `distlib`.

Four test exeutables are created from the following 2x2 matrix:

+----------+------------------------+
| Console  | OS-installed Python    |
+----------+------------------------+
| Windowed | Same Python, in a venv |
+----------+------------------------+

The venv is created in the `env` subdirectory using the OS-installed Python using
`python -m venv env` and `distlib` and `psutil` are installed into it using `pip install`.

The test executables differ only in the launchers used (console - `t64.exe`, or windowed
- `w64.exe`) and their shebangs. The scope of the tests is currently 64-bit only. The
executables are named as follows:

+--------------+-------------------------------------------------------------------+
| `test.exe`   | Console executable, using the OS-installed Python in the shebang  |
+--------------+-------------------------------------------------------------------+
| `testw.exe`  | Windowed executable, using the OS-installed Python in the shebang |
+--------------+-------------------------------------------------------------------+
| `testv.exe`  | Console executable, using the venv's Python in the shebang        |
+--------------+-------------------------------------------------------------------+
| `testvw.exe` | Windowed executable, using the venv's Python in the shebang       |
+--------------+-------------------------------------------------------------------+

The script to make the tests - `make_launcher_tests.py` - needs distlib to get access to
its launchers. The script to run the tests - `run_launcher_tests.py` - needs `psutil` to
examine subprocess trees.

The `make_launcher_tests.py` script is used to make the test executables in the `test`
subdirectory. Invocation options are:

.. raw:: html

    <pre>
    $ python make_launcher_tests.py -h
    usage: make_launcher_tests [-h] [-p PYTHON] [-o OUTDIR] [-s SUFFIX]

    optional arguments:
      -h, --help            show this help message and exit
      -p PYTHON, --python PYTHON
                            Use this in the shebang - must contain the text "python.exe" (default: env\scripts\python.exe)
      -o OUTDIR, --outdir OUTDIR
                            Write files here (default: test)
      -s SUFFIX, --suffix SUFFIX
                            Suffix for executables (default: v)
    </pre>

The `run_launcher_tests.py` script is used to run the tests. Invocation options are:

.. raw:: html

    <pre>
    $ python run_launcher_tests.py -h
    usage: run_launcher_tests [-h] [--delay DELAY] [--console] [--windowed] [-s SUFFIX]

    optional arguments:
      -h, --help            show this help message and exit
      --delay DELAY, -d DELAY
                            Delay before trying to stop (default: 5)
      --console, -c         Test console executable only (default: False)
      --windowed, -w        Test windowed executable only (default: False)
      -s SUFFIX, --suffix SUFFIX
                            Suffix for executables (default: v)
    </pre>
