# mathagents.org

The website for the MathAgents workshops: one static page, served by GitHub Pages at <https://mathagents.org>.

There is no build step. `index.html` is the page (the figure at the top is inline SVG), `style.css` its styles with the colours as variables at the top, and `fonts/` holds the two typefaces (Source Serif 4 and Source Sans 3, under the SIL Open Font License: `fonts/OFL.txt`).

## Adding or changing a workshop

Each workshop is one `<li class="event">` block in `index.html`. To add one, copy a block into the **Upcoming workshops** list, in date order, and edit it:

```html
<li class="event" data-starts="2027-02-06" data-ends="2027-02-06">
  <p class="when"><time datetime="2027-02-06">February 6, 2027</time> <span>Saturday</span></p>
  <div class="what">
    <h3>City, ST</h3>
    <p><a href="https://example.edu/event"><cite>Title of the workshop</cite></a> at the host, for whom.</p>
  </div>
  <p class="who">Organized by A, B and C</p>
</li>
```

- `data-starts` and `data-ends` are `YYYY-MM-DD`. For a one-day workshop they are the same.
- You don't move workshops to **Past workshops** by hand. A short script at the bottom of `index.html` does it in the reader's browser on the day after `data-ends`, and labels the earliest upcoming date "Next". (Without JavaScript, the page shows the lists as they are written in the file.)
- A workshop with no web page yet has no link: see the ICERM entry.

## Previewing a change

```bash
python3 -m http.server 8000    # then open http://localhost:8000
```

## Hosting

- **GitHub Pages:** in the repository's *Settings → Pages*, set the source to *Deploy from a branch*, branch `main`, folder `/ (root)`, and the custom domain to `mathagents.org`. The `CNAME` file in this repository holds the same domain, and `.nojekyll` tells Pages to serve the files as they are.
- **DNS** for `mathagents.org` (at the registrar):

  | Type | Host | Value |
  |---|---|---|
  | A | `@` | `185.199.108.153` |
  | A | `@` | `185.199.109.153` |
  | A | `@` | `185.199.110.153` |
  | A | `@` | `185.199.111.153` |
  | AAAA | `@` | `2606:50c0:8000::153` |
  | AAAA | `@` | `2606:50c0:8001::153` |
  | AAAA | `@` | `2606:50c0:8002::153` |
  | AAAA | `@` | `2606:50c0:8003::153` |
  | CNAME | `www` | `mathagents.github.io` |

  These are the addresses in GitHub's guide, [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site). Records for other subdomains are not affected.
- Once the DNS check in *Settings → Pages* passes, tick **Enforce HTTPS**.
