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

## Common options

- `-t NAME` sets the table name.
- `-pk COLUMN` sets a primary key.
- `-i COLUMN` adds an index.
- `-f COLUMN` adds a full-text search index.
- `--replace-tables` replaces existing tables.
- `--just-strings` imports all values as text.

Run `csvs-to-sqlite --help` to see every option.

## License

Apache License 2.0. See [LICENSE](LICENSE).
