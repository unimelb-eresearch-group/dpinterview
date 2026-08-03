# GitHub actions

Currently only defines a dependabot config for `uv` using a [`pkl`](https://pkl-lang.org) template. For a breakdown of
how this works [see this blog post](https://pkl-lang.org/blog/how-we-manage-github-actions.html). It is only necessary
to install and understand pkl to update the workflows (of which there are currently none) or `dependabot.yml`.

Using `pkl` is more complex than strictly necessary, however, it adds a layer of validation and type checking not
present when hand rolling YAML files.

## Working with pkl workflows

### Setup

Simply [install pkl](https://pkl-lang.org/main/current/pkl-cli/index.html#installation) as appropriate for your system.
All the pkl files needed either live in `.github` or are dependencies defined in `.github/PklProject`.

### Build

To generate the actions configs run:

```shell
# Update dependencies
pkl project resolve .github/
# Generate `.yml` files
pkl eval -m .github/   --project-dir .github/ .github/index.pkl
```

alternatively use the `mise` tasks provided if using `mise`

```shell
mise run generate:workflows 
```

then commit any added, updated, or generated files in `.github/`

### Adding New Workflows

The [blog post mentioned earlier](https://pkl-lang.org/blog/how-we-manage-github-actions.html) is a reasonable primer on
developing a pkl based workflow. To understand how workflows work
[the official documentation](https://docs.github.com/en/actions) is a good starting point. It's quite likely you'll
rapidly run out of actions already modelled in pkl from the
[provided set](https://pkl-lang.org/package-docs/pkg.pkl-lang.org/pkl-pantry/com.github.actions/current/index.html)
in which case
the [action generator](https://pkl-lang.org/package-docs/pkg.pkl-lang.org/pkl-pantry/com.github.actions.contrib/current/index.html)
is the next port of call.

