# pysqlite3

This library takes the SQLite module from Python 3 and packages it as a
separately-installable module. The binary package is statically compiled
which make it easy to embedded the library in certain circumstances.

This may be useful for creating SQLite modules capable of working with other
versions of SQLite (via the amalgamation option). Meanwhile, the included SQLite
library is compiled with **all features enabled**, that user may benefit from
more features, like the score based database FTS (Full-Text Search).

Additional features:

* User-defined window functions (requires SQLite >= 3.25)
* Flags and VFS an be specified when opening connection
* Incremental BLOB I/O, [bpo-24905](https://github.com/python/cpython/pull/271)
* Improved error messages, [bpo-16379](https://github.com/python/cpython/pull/1108)
* Simplified detection of DML statements via `sqlite3_stmt_readonly`.
* Sqlite native backup API (also present in standard library 3.7 and newer).

A completely self-contained binary package (wheel) is available for versions
0.5.1 and newer as `pysqlite-binary`. This package contains the latest release
of SQLite compiled with numerous extensions, and requires no external
dependencies.

# Using the binary package

A binary package (wheel) is available for Windows/Linux/macOS with a completely
self-contained `pysqlite3`, statically-linked against the most recent release
of SQLite.

```bash
pip install pysqlite-binary
```

# Building a statically-linked library

To build `pysqlite3` statically-linked against a particular version of SQLite,
you need to obtain the SQLite3 source code and copy `sqlite3.c` and `sqlite3.h`
into the source tree.

A build plugin is implemented to automatically download the amalgamation source
code from official website. If you want to compile against a specific version,
The SQLite version number is controlled through `SQLITE_VERSION`
variable in [setup.py#L22](https://github.com/pysqlite3/pysqlite3/blob/3fe3828cfd46407a9afeee3a76d8839b1cd759a2/setup.py#L22).

```
python setup.py build_ext build
```

You now have a statically-linked, completely self-contained `pysqlite3`.

# Building with System SQLite

To build `pysqlite3` linked against the system SQLite, run:

```
python setup.py build_dynamic
```
