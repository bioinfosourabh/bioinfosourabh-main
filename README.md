# bioinfosourabh.netlify.app

Source of the personal academic website of **Sourabh Kumar**, bioinformatics scientist working on clinical cancer and germline genomics.

Live site: <https://bioinfosourabh.netlify.app>

## Contents

The site presents my research profile, publications, projects and talks. My code is on GitHub: see <https://github.com/bioinfosourabh>, which lists the analysis pipelines (HRD scoring, TMB/MSI, CNV, variant calling, pharmacogenomics, transcriptomics) and machine-learning projects.

## Build

The site is built with [Hugo](https://gohugo.io/) (version pinned in `netlify.toml`) using the [Hugo Apéro](https://github.com/hugo-apero/hugo-apero) theme, and is deployed automatically by Netlify on each push to `main`.

To preview locally:

```bash
git clone --recurse-submodules https://github.com/bioinfosourabh/bioinfosourabh-main
cd bioinfosourabh-main
hugo server
```

Then open <http://localhost:1313>.

| Path | Purpose |
|---|---|
| `config.toml` | site settings, menus and social links |
| `content/` | pages: about, publications, projects, talks, blog |
| `static/` | images and other static files |
| `themes/hugo-apero/` | theme |
| `netlify.toml` | Netlify build settings |

## Credits

The layout is based on the Hugo Apéro theme by Alison Hill and on an open-source personal site template; the content is my own.

## Contact

Sourabh Kumar · bioinfosourabh@gmail.com · ORCID [0009-0009-5840-9830](https://orcid.org/0009-0009-5840-9830)
