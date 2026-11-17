# Data

The analysis uses patents published by the European Patent Office (EPO) in 2023. The data was provided in the course and is **not included** in this repository, because the patent records contain personal data (inventor names and addresses).

## Files the notebook expects

Put both zip files in `data/raw/` (this folder is ignored by Git):

| File | Content |
|---|---|
| `data/raw/2023_title_publ_inventor.zip` | one CSV (`2023_title_publ_inventor.csv`) with about 98k patent records, one row per publication, 12 columns |
| `data/raw/2023_ipc_codes.zip` | about 91k text files named `<patent_id>_ipc.txt`, each listing the IPC codes of one patent (one code per line) |

The notebook only uses these columns and fields:

- `publication.number`: patent id, used to match the two files
- `applicant`: list of applicants with their country; the country of the first applicant is used
- the IPC codes, shortened to their main group (for example `G01R33/561` becomes `G01R33`)

## IPC codes

The International Patent Classification is maintained by WIPO: https://www.wipo.int/ipc/en/. The code descriptions in the notebook (for example in the top-20 ubiquity chart) come from there.
