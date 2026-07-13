# csvs-to-sqlite

Convert CSV files into a SQLite database from the command line.

## Installation

```bash
pip install csvs-to-sqlite
```

## Usage

```bash
csvs-to-sqlite myfile.csv mydatabase.db
```

This creates `mydatabase.db` with a table named `myfile`.

Pass several files to create several tables:

```bash
csvs-to-sqlite one.csv two.csv bundle.db
```

Wildcards and directories are also supported:

```bash
csvs-to-sqlite ~/Downloads/*.csv my-downloads.db
csvs-to-sqlite ~/path/to/directory all-my-csvs.db
```
### TSV files

Use `-s` to set a different separator:

```bash
csvs-to-sqlite my-file.tsv my-file.db -s $'\t'
```

### Lookup tables

Use `-c` to extract a column into a separate lookup table:

```bash
csvs-to-sqlite data.csv -c category output.db
```

## csvs-to-sqlite --help

<!-- [[[cog
import cog
from csvs_to_sqlite import cli
from click.testing import CliRunner
runner = CliRunner()
result = runner.invoke(cli.cli, ["--help"])
help = result.output.replace("Usage: cli", "Usage: csvs-to-sqlite")
cog.out(
    "```\n{}\n```".format(help)
)
]]] -->
```
Usage: csvs-to-sqlite [OPTIONS] PATHS... DBNAME

  PATHS: paths to individual .csv files or to directories containing .csvs

  DBNAME: name of the SQLite database file to create

Options:
  -s, --separator TEXT            Field separator in input .csv
  -q, --quoting INTEGER           Control field quoting behavior per csv.QUOTE_*
                                  constants. Use one of QUOTE_MINIMAL (0),
                                  QUOTE_ALL (1), QUOTE_NONNUMERIC (2) or
                                  QUOTE_NONE (3).
  --skip-errors                   Skip lines with too many fields instead of
                                  stopping the import
  --replace-tables                Replace tables if they already exist
  -t, --table TEXT                Table to use (instead of using CSV filename)
  -c, --extract-column TEXT       One or more columns to 'extract' into a
                                  separate lookup table. If you pass a simple
                                  column name that column will be replaced with
                                  integer foreign key references to a new table
                                  of that name. You can customize the name of
                                  the table like so:     state:States:state_name
                                  
                                  This will pull unique values from the 'state'
                                  column and use them to populate a new 'States'
                                  table, with an id column primary key and a
                                  state_name column containing the strings from
                                  the original column.
  -d, --date TEXT                 One or more columns to parse into ISO
                                  formatted dates
  -dt, --datetime TEXT            One or more columns to parse into ISO
                                  formatted datetimes
  -df, --datetime-format TEXT     One or more custom date format strings to try
                                  when parsing dates/datetimes
  -pk, --primary-key TEXT         One or more columns to use as the primary key
  -f, --fts TEXT                  One or more columns to use to populate a full-
                                  text index
  -i, --index TEXT                Add index on this column (or a compound index
                                  with -i col1,col2)
  --shape TEXT                    Custom shape for the DB table - format is
                                  csvcol:dbcol(TYPE),...
  --filename-column TEXT          Add a column with this name and populate with
                                  CSV file name
  --fixed-column <TEXT TEXT>...   Populate column with a fixed string
  --fixed-column-int <TEXT INTEGER>...
                                  Populate column with a fixed integer
  --fixed-column-float <TEXT FLOAT>...
                                  Populate column with a fixed float
  --no-index-fks                  Skip adding index to foreign key columns
                                  created using --extract-column (default is to
                                  add them)
  --no-fulltext-fks               Skip adding full-text index on values
                                  extracted using --extract-column (default is
                                  to add them)
  --just-strings                  Import all columns as text strings by default
                                  (and, if specified, still obey --shape,
                                  --date/datetime, and --datetime-format)
  --version                       Show the version and exit.
  --help                          Show this message and exit.

```
<!-- [[[end]]] -->
