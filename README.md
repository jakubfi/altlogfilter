
AltLogFilter is a small tool to filter out those tons of messages that Altera Quartus II
commandline tools produce. Useful for making sane makefiles for Altera projects that don't
need a GUI for development.

Usage
==========================================================================

```
alf [-h] [-f FILTER] [-n] [-d] [-S] [-c] command [options]
```

Positional arguments:

* **command** - Altera command (with arguments) which output should be filtered

Optional arguments:

* **-h, --help** - show this help message and exit
* **-f FILTER, --filter FILTER** - Suppression filter
* **-n, --nodefault** - Ommit default filters
* **-N, --nothing** - Suppress nothing (ommit all filters - default and specified)
* **-d, --debug** - Enable filter debug
* **-S, --stats** - Show suppression statistics
* **-c, --color** - Use colored output

You can also set NALF environment variable to "1" to stop any suppression (equivalent of using -N argument)

Filters
==========================================================================

You may use any number of Filters. Each filter is of form:

```
level:id:min_indent_level
```

where:

* **level** - message level (Info, Extra Info, Warning, Critical Warning, Error)
* **id** - numerical message ID
* **min_indent_level** - minimum indentation level on which message occurs

Suppression filters enabled by default:

* **Info::** - suppress all informational messages
* **Extra Info::** - suppress all extra informational messages
* **:20028:** - suppress "Parallel compilation is not licensed" warning
* **:292013:** - suppress "Feature LogicLock is only available with a valid subscription license" warning
* **:332012:** - suppress "Synopsys Design Constraints File file not found" warning
* **::1** - suppress all messages on indentation level 1 or above

Example usage
==========================================================================

```
alf -c -S -- quartus_map --no_banner --64bit --family=CycloneII my_project
alf -n -s :209061: -- quartus_pgm --64bit -c 1 -m JTAG -o "p\;output_files/my_project.sof"
```
