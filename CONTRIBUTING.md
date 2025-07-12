# Development

The website is built with [zine](https://github.com/kristoff-it/zine).
You can install it from binary or build it from source, as detailed in the [quickstart](https://zine-ssg.io/quickstart/).

## Content ownership

Event organizers are free to manage content for their Zig Day pages using [GitHub's CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners).

The GitHub handles that are listed next to a repository path allow organizers to merge autonomously the content changes made via pull requests.

## Build the site locally

Once the `zine` binary is in your PATH, you can see a local version of the webiste by running

```
zine
```

in the root directory of this repository.

The command output will show a link to browse the website locally.

## Adding an event

Events are integer-indexed files, and they are located into a `content/<region>/<city>` directory.
To create a new event, create an `<X>.smd` file in the directory, replacing `X` incrementing the event counter.

There is not a pre-defined format for the content of the `X.smd` file.
Fill it in with the information that is useful to attend the event, such as venue address, event activities, etc...







