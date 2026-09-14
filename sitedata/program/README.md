# Program paper CSV files

Use one CSV file for the papers in each program session. Store the files in this directory:

`sitedata/program/`

## Required CSV headers

Every file must contain these headers exactly:

```csv
paper_id,paper_name,authors,paper_type,presentation_mode
```

The fields are:

- `paper_id`: Internal identifier for the paper.
- `paper_name`: The paper title shown on the program page.
- `authors`: Author names. Separate multiple authors with commas or semicolons.
- `paper_type`: The paper type shown on the program page, for example `long`, `short`, or `already published`.
- `presentation_mode`: Internal information such as `Accept (Oral)` or `Accept (Poster)`. This is not shown publicly.

## Example CSV

```csv
paper_id,paper_name,authors,paper_type,presentation_mode
72,Mid-Utterance Transition Control for Audio Commentary Generation,"Ryota Kawamatsu, Tatsuya Ishigaki, Hiroya Takamura",long,Accept (Oral)
```

If a value contains a comma, surround the complete value with double quotes. This is especially important for the `authors` field and paper titles containing commas.

For names containing semicolons, use commas as the separator instead:

```csv
p001,Example paper,"Alice Smith, Bob Jones",short,Accept (Oral)
```

## Connect a CSV to a session

Add `papers_file` to the relevant session in `sitedata/program.yml`. The path is relative to `sitedata/`:

```yaml
- time: 09:10-10:40
  title: Oral session 1
  papers_file: program/oral_1.csv
```

Do not add a manually written `papers` list when using `papers_file`. The site loads the paper rows automatically.

## Adding a new session file

1. Create a CSV file in `sitedata/program/`.
2. Add the five required headers.
3. Add one row per paper.
4. Reference the file with `papers_file` in `sitedata/program.yml`.
5. Run `make freeze` to regenerate the static site.

The public program displays the paper type, title, paper ID, and authors. The `presentation_mode` value is loaded for internal use but is intentionally not displayed.
