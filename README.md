# ctf4nuclear landing page

Source for the public landing page of the **CTF4Nuclear MSFR** NeurIPS 2026 competition:

→ <https://ctf-for-science.github.io/ctf4nuclear/>

The site is a single-page Jekyll build using the `cayman` theme; GitHub Pages renders `index.md` automatically on every push to `main`. Most updates need only an edit to `index.md`.

## Local preview (optional)

```bash
bundle init
bundle add jekyll
bundle add github-pages
bundle exec jekyll serve
```

Then open <http://localhost:4000/ctf4nuclear/>.

## License

Site content: CC-BY-4.0. Site code: MIT.
