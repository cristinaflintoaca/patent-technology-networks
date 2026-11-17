# Patent technology networks

Which countries are really alike in what they invent and which similarities only appear because some countries patent in almost everything?

In this project I used the patents published by the European Patent Office (EPO) in 2023 to build a network of countries and technologies. I then used a statistical null model to keep only the links between countries that are stronger than chance.

## The approach

- I started from about 98k patent records and their technology codes (IPC). Each code was shortened to its main group (for example `G01R33/561` becomes `G01R33`) and each patent was assigned to the country of its first applicant.
- I kept countries with at least 10 patents and technology codes used by at least 3 countries. This left 57 countries and 3469 technology codes.
- To compare small and large countries fairly, I used the Revealed Technological Advantage (RTA). A country counts as specialized in a technology when that technology's share of its patents is higher than its share worldwide (RTA > 1).
- From this country–technology network I built two networks of countries:
  - a naive one, where two countries are linked if they share at least one specialization
  - a validated one using the Bipartite Configuration Model (BiCM) which keeps a link only if the overlap is larger than expected by chance (α = 0.05)
- Finally, I looked for groups of countries in the validated network with the Louvain algorithm and described each group by the technologies its members share.

## Results

| | Naive network | BiCM-validated network |
|---|---|---|
| Links | 1,494 | 73 |
| Density | 0.94 | 0.05 |
| Average degree | 52.4 | 2.6 |
| Connected components | 1 | 25 |
| Average clustering | 0.95 | 0.18 |

The validated network splits into four groups of countries (modularity Q = 0.37):

| Group | Countries | Shared technologies |
|---|---|---|
| Digital & computing | BB, CA, CZ, FI, FR, IL, IN, LT, NO, PL, RO, SE, SG, TW | network services, cryptography, IT security, image recognition |
| Pharma & biotech | AU, BR, CL, CU, HK, KY, MX, PT, RU, SA, SI, VG | nervous system drugs, peptides, medicines, genetic engineering |
| Pharma & tech bridge | AE, BM, GR, HU, IE, MT | medicines, surgical instruments, machine learning |
| Construction materials | BG, LI | cement and building materials, building construction |

## Main take-aways

- The naive network is almost complete: 94% of all possible country pairs are linked, so it shows almost no structure.
- After validation only 73 links are left (95% removed). These are the overlaps that are larger than chance.
- The biggest patent filers (US, Japan, China, Germany, South Korea, UK, Italy, Spain and the Netherlands) end up with no links at all. They are specialized in so many technologies that sharing some with any other country is expected, not surprising.
- All four groups are made up of smaller and mid-sized patent filers and each is held together by a fairly narrow set of technologies.
- Singapore is the most important bridge between countries (highest betweenness) while Cuba has the most direct links (11).

## Limitations

- Only patents published in 2023.
- Each patent counts only for the country of its first applicant.
- Some applicant countries, such as the Cayman Islands (KY), the British Virgin Islands (VG) and Bermuda (BM), are places where companies are registered rather than where the research happens.
- The groups come from a single Louvain run, without checking how stable they are.

## Repo structure

```text
notebooks/patent_network_analysis.ipynb   the full analysis
data/README.md                            where the data comes from
```

## How to run it

```bash
pip install -r requirements.txt
```

The raw patent data is not included because it contains inventor names and addresses (see `data/README.md`). Put the two zip files in `data/raw/` and run the notebook.

## References

- Saracco, F., Di Clemente, R., Gabrielli, A., & Squartini, T. (2017). Inferring monopartite projections of bipartite networks: an entropy-based approach. New Journal of Physics, 19(5), 053022.
- Soete, L., & Wyatt, S. (1983). The use of foreign patenting as an internationally comparable science and technology output indicator. Scientometrics, 5(1), 31–54.
- OECD (2009). OECD Patent Statistics Manual. OECD Publishing, Paris.
- WIPO. International Patent Classification (IPC).

## Background

Individual final project for the course Network Science (MSc Social and Economic Data Science, 2026).
