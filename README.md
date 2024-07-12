# handyman5's blog

Live at <https://handyman5.github.io/>

This is the source for my personal website and blog. It's using [Nikola](https://getnikola.com/). Feel free to inspect it and see how the sausage is made.

## Development

Running a local copy is as simple as:

``` shell
$ python3 -m venv .venv
$ source .venv/bin/activate
$ pip install 'Nikola[extras]'
$ nikola build
$ nikola serve
```

The site will be available at <http://localhost:8000>.

To update the site, re-run `nikola build`; the `serve` process will automatically notice and serve the new files.

## Structure

This is the directory structure:

```
.
├── files
├── images
├── pages
├── plugins
├── posts
└── themes
    └── kiss
        ├── assets
        │   └── css
        └── templates
```

* `files`: files that are incorporated by the build process into the generated site
* `images`: images used in the site, including the logo
* `pages`: undated text files referencing specific fixed topics
* `posts`: dated text files (primarily Markdown) each containing a blog post
* `themes`: I started with [the kiss theme](https://themes.getnikola.com/v8/kiss/) but I've modified it fairly heavily

## Deployment

The site is hosted at Github Pages. See [.github/workflows/main.yaml] for the deployment workflow. It is set up to run with every commit automatically.

## Commands

| Command | Action |
| --- | --- |
| `nikola build` | Builds a static copy of the site |
| `nikola serve` | Serves the current website on `localhost:8000` |
