# Site maintenance and deployment

## Architecture and modified files

- `_config.yml`: identity, canonical project-site URL, `/ChaoHe-research` baseurl, plugin feature flags, Scholar author matching, demo output disabled, documentation/tool exclusions.
- `_bibliography/papers.bib`: complete Endo-GSG and Endo-4SRF citations.
- `_data/accepted_papers.yml`: incomplete accepted ROBIO record; no author or DOI fabricated.
- `_data/socials.yml`, `_data/news.yml`: verified contact and news content.
- `_pages/about.md`, `_pages/publications.md`, `_pages/404.md`: public pages.
- `_includes/publication-list.liquid`, `_includes/publication.liquid`: shared list and optional-metadata component.
- `_layouts/academic.liquid`, `_layouts/academic_bib.liquid`: new site-specific layouts using the existing default shell and Jekyll Scholar.
- `assets/css/academic.scss`, `assets/img/favicon.svg`: site styling and initials favicon.
- `_includes/head.liquid`, `_includes/header.liquid`: two intentional, audited overrides. Head uses system fonts with no Google Fonts request, accurate metadata and canonical links; header uses a compact, keyboard-accessible two-link navigation without requiring a mobile script. Plugin gem files are untouched.
- `.al-folio-overrides.yml`: reviewed upstream checksums for drift detection.
- `.github/workflows/deploy.yml`: retains the upstream build/purge/deploy architecture; explicitly targets `gh-pages` and disables force-push. Template maintenance workflows are restricted to the upstream repository so they cannot regenerate demo content or run unrelated scheduled jobs here.
- `AGENTS.md`, `RESEARCH_NOTES.md`, `README.md`, `.gitignore`: site rules, evidence, local instructions, isolated toolchain exclusion.

Template blog posts, projects, news, books, teaching, CV data/assets, portraits,
example bibliography, extra social profiles and demo navigation pages were removed.
Their framework plugins and collection declarations remain available.

## Visual structure

The site uses a pale slate page background with white, lightly bordered sections,
navy headings and readable secondary text. Research interests and News share a row
on desktop and stack on small screens. Publications remain a single academic list;
venue labels use pale blue, and the user-confirmed ROBIO finalist label uses a muted
warm accent. No shadows, decorative images or animation dependencies were added.

The visual review compared [Jon Barron](https://jonbarron.info/),
[Deepak Pathak](https://www.cs.cmu.edu/~dpathak/) and [Keunhong Park](https://keunhong.com/).
These informed hierarchy and section separation; their content/assets are not reused.
Site colors and spacing live in `assets/css/academic.scss`. Main text color pairs
have at least 6.3:1 contrast. Both public pages were checked at 1440/1024/768/390px,
including expanded BibTeX, missing-author behavior, focus navigation and asset loads.

## Add a publication

Add a verified record to `_bibliography/papers.bib`. Use `selected = {true}` to
show it in the shared list (currently all authorized papers are selected).
Records appear in file order, followed by incomplete accepted records. The
current order is Endo-GSG, Endo-4SRF, then ROBIO. Both pages share the same include.

Use native BibTeX `author = {Last, First and Last, First}` in the original order;
never insert markup. `_config.yml` matches first name `Chao`, last name `He` and
the component uses `<strong>` for this exact match only. `abbr` is the full visible
venue label, including year. Use `journal`, `volume`, `number`, `pages` for journal
citations; `booktitle`, optional `series`, `pages` for conferences.

An accepted paper without confirmed authors belongs only in
`_data/accepted_papers.yml`. When its complete citation becomes available, move it
to BibTeX and remove the YAML record so it cannot appear twice. Do not add private
submissions or unapproved publication metadata anywhere in the public source.

Optional fields: `html` (official Paper page), `pdf` (authorized public URL), `doi`,
`code` (real repository), `website` (real project page), and `video`. Absent fields
produce no links. BibTeX uses native keyboard-accessible `<details>`.

## Add a teaser

Place an authorized image in `assets/img/publication_preview/`, then add
`preview = {filename.png}` and `preview_alt = {Specific scientific description}`
to its record. Accepted YAML records support the same fields. Use a compressed
image approximately 460 pixels wide or larger for high-density displays; preserve
labels, captions and aspect ratio. The layout reserves about 220 pixels on desktop,
uses `object-fit: contain`, and stacks on mobile. Without an image, the record is
text-only without an empty thumbnail box. No current teaser has confirmed reuse
permission; provide authorized figures for all three papers. Do not use AI images.

## Projects and CV

Projects: add authentic content to `_projects/`, enable `collections.projects.output`,
and add a real `_pages/projects.md` using the core `page` layout when ready. Keep
`nav: false` until content is complete. Add its navigation link to the intentionally
small `_includes/header.liquid`. For pages requiring math, video or other plugin
styles, extend the site head with the owning plugin's documented hooks; the present
head deliberately only loads the current site's CSS.

CV: add an authentic PDF under `assets/pdf/`, then add a labeled link to that file
using `relative_url`. Add a CV nav link only once the PDF exists. No CV, dates,
degrees or employment history should be inferred from the current biography.

## GitHub deployment

SSH authenticated as `Hansello218`. The user created the original empty
`Hansello218.github.io` repository, then chose the project-site name
`ChaoHe-research`. The GitHub-side rename has now been completed and verified with a successful
`git ls-remote origin` returning no refs (empty repository). Local `origin`
targets the new name. Source has been pushed to `main` with user authorization. Deploy run
[44280380472](https://github.com/Hansello218/ChaoHe-research/actions/runs/44280380472)
succeeded for source `12bab4b`, publishing generated files to `gh-pages` (`f3cc66f`).
The generated branch was checked for correct publication content and asset paths.
GitHub Pages was activated by the user with `gh-pages / (root)`. Official Pages
run [44281146540](https://github.com/Hansello218/ChaoHe-research/actions/runs/44281146540)
succeeded. The homepage, Publications page and stylesheets now return HTTP 200.

1. Open the existing `Hansello218/Hansello218.github.io` repository on GitHub.
   Go to Settings → General → Repository name, enter **ChaoHe-research**, and
   select Rename. The final repository should be `Hansello218/ChaoHe-research`.
   Do not initialize or add files before the first source push.
2. In Settings → Actions → General, allow the workflow's actions and select
   **Read and write permissions** under Workflow permissions. The deploy workflow
   also declares `contents: write`; organization/account policy must permit it.
3. After reviewing the local changes, publish manually:

   ```bash
   cd /home/chao/Downloads/workplace/code/Hansello218.github.io
   git status --short
   git remote -v
   git add -A
   git commit -m "Build Chao He's academic homepage"
   git push -u origin main
   ```

   `origin` is `git@github.com:Hansello218/ChaoHe-research.git`.
   `upstream` records the official template provenance. Push only to `origin`.
   If the remote acquires commits in the meantime, fetch and review them first;
   do not force-push over them.

4. Wait for **Deploy site** in Actions to pass and create `gh-pages`. The workflow
   runs Jekyll with Ruby 3.3.5 on Ubuntu 24.04, preserves `baseurl: /ChaoHe-research`, purges CSS, and publishes
   generated `_site` to `gh-pages` without force-push.
5. Settings → Pages → Source: **Deploy from a branch**; select **gh-pages** and
   **/(root)**, save, and enable HTTPS once available. Do not choose the `main`
   branch. The publishing folder is still **/(root)** of `gh-pages`; GitHub adds
   the project URL prefix automatically. Visit <https://hansello218.github.io/ChaoHe-research/>.

A scheduled template workflow being skipped is intentional. The existing formatter
and upgrade audit remain active. GitHub-side execution and HTTPS issuance cannot
be verified until the repository is renamed and the source is pushed.

## Validation (2026-11-18)

- Production Jekyll build succeeded with the pinned bundle; native BibTeX parsing succeeded.
- `npm ci` and `npm run lint:prettier` passed.
- `al-folio upgrade audit`: zero blocking and zero non-blocking findings.
- `al-folio upgrade overrides audit`: two reviewed/acknowledged overrides, no stale override.
- Chromium inspected `/` and `/publications/` at 1440, 1024, 768 and 390 pixels. Each view contains exactly three papers in the required order; no horizontal overflow, broken requests or page script errors. Tested BibTeX expansion and keyboard skip link. Desktop and mobile screenshots visually reviewed.
- Tested generated CSS after the same PurgeCSS step used by deployment.
- Verified canonical links, internal assets, author order/highlighting, accurate DOI strings, missing-author behavior, absence of fake links and template navigation, and generated public page routes. No portrait or teaser references remain.
- Official sources: [IJCAI](https://www.ijcai.org/proceedings/2026/129) and [PubMed](https://pubmed.ncbi.nlm.nih.gov/40030513/). IEEE's document page required a robot check; ROBIO acceptance is user-confirmed, with no public DOI or author list supplied.

Missing: authorized publication teasers, ROBIO complete author list and official
publication links, an authentic CV PDF (optional). GitHub Actions deployment to `gh-pages` has succeeded. Public hosting has been verified with HTTP 200 responses, correct content and
stylesheet availability; Safari/Firefox browser behavior has not been tested.
