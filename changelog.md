# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).


## [git] - 2020-03-12
### Added
- Handle Minetest Lua tracebacks (such as from debug.txt or stderr)
  (requires fix below)

### Fixed
- Handle `PARSE_MARKER_FILE` value not at the start of a line.


## [git] - 2020-03-11
### Added
- Allow simpler syntax while avoiding false positives by only allowing
  the param opener when it is followed by a digit.
  - Detect grep output syntax.
  - Detect nose test output syntax without hard-coded `split(":")`.


## [git] - 2019-12-27
### Changed
- Fix pycodestyle support.
- Improve changelog formatting and grammar.


## [git] - 2019-01-11
### Changed
- Make parsing modes into modular, expandable datasets.
- Use clang-format for coding style.


## [git] - 2018-01-11
### Added
- Support nosetests output.


## [git] - 2018-08-15
### Changed
- Warn if input file is missing or has only blank lines.
- Allow a param to specify output (continue to use err.txt as default).


## [git] - 2017-11-09
### Added
- Detect and show fatal errors (with an explanation that your tool
  recorded them before outputinspector started, to avoid any confusion)


## [git] - 2017-11-09
### Changed
- Drastically improve install script (detect and warn if it can't
  manipulate existing install in any way, and installs to /usr/local/bin
  instead of /usr/bin).
  - Detect and stop installing if /usr/bin/outputinspector exists,
    (should be /usr/local/bin) and show repair instructions (see install
    file echo statements for more details).
  - Detect newer version (whether Debug or Release).
  - If neither Debug nor Release is present (in Qt Creator default build
    folders), use outputinspector binary in working directory if
    present, otherwise show error and exit.
    - If no source binary is found, give instructions on how to proceed
      (also, instructions for recompiling on success now correctly state
      to use Qt Creator instead of QtDevelop).


## [git] - 2017-11-09
### Added
- Try to detect and convert jshint output to mcs output:
  - example output of running 'mcs etc/foo.cs 1>out.txt 2>err.txt  if you have mcs installed (the c# compiler which normally comes with the mono package, or can also be from a .NET Framework SDK or other C# development tool)':
```
etc/foo.cs(10,24): error CS0103: The name `Path' does not exist in the current context
Compilation failed: 1 error(s), 0 warnings
```

    or with line 10 commented:
```
etc/foo.cs(11,20): warning CS0219: The variable `uhoh' is assigned but its value is never used
Compilation succeeded - 1 warning(s)
```

    or if file doesn't exist:
```
error CS2001: Source file `etc/foo.cs' could not be found
```
  - jshint example output (result of running jshint etc/foo.js if you have jshint installed):
```
etc/foo.js: line 2, col 9, Use '!==' to compare with 'null'.

1 error
```


## [first qt5 version] - 2017-03-25
### Changed
- Change old code (had MainWindow, listMain, menubar, and statusbar):
  - Change menubar to menuBar.
  - Change statusbar to statusBar.
  - Change listMain (in old code) to ui->mainListWidget (rename in new
    code from listWidget which was present by default for new widget
    form).
  - Deprecate manually resizing list widget (in favor of sizePolicy
    Expanding [and default aka MAX_INT maximumSize] for both vertical
    and horizontal).
- Change new code (had MainWindow, centralWIdget, menuBar, mainToolBar
  and statusBar all by default for new widget form; don't rename
  anything):
  - Create a List Widget (QListWidget, and Item-Based Widget) named
    mainListWidget.
  - Right-click mainListWidget in form designer, go to slot, paste
    content of QListWidget::itemDoubleClicked from old qt4 version.


## [git] - 2017-03-25
### Changed
- Move from sourceforge to GitHub.


## [Unreleased] - 2008-10-qt4
- Known Issues with this sf.net release:
  - At least in Kate 3.0.3, "kate -u" becomes ineffective when Kate 2 is
    open at the same time, so more copies of Kate 3 open.

### Changed
(for configurable settings, edit the variable name in /etc/outputinspector.conf)
- Open source files and look for TODO comments (FindTODOs=yes in conf
  file).
- Allow auto-close if no errors occur (ExitOnNoErrors=yes in conf file).
- Show count of errors and warnings (and TODOs unless specified -- see
  above) in status bar.
- Fix problem caused by Kate line & row args starting with zero
  (configurable: by default xEditorOffset=-1 and xEditorOffset-1).
- Kate is no longer linked as a child process of outputinspector.
- Compensate for different tab handling between Kate 3 and mcs, and
  attempt to work around Kate 2 tab traversal glitches related to the
  column command line parameter (see README.md).


## [qt4 (Initial release)] - 2008-09-30
- Known issues with this sf.net release:
  - kate 2.5.x, Kate 3.0.x, and mcs all have different ways of counting
    tabs, so column numbering is not exact.

### Changed
- Open err.txt if in the same folder as outputinspector (see README
  under "Usage").
- If user double-clicks a line of code, tell kate to navigate to that
  file and location, as long as the file (or relative path) is in the
  same folder as outputinspector and err.txt.

### Added
- Handle kate (at least 2.5.9) as it does not go to the exact code
  location since -l and -c args start at origin (0,0).
