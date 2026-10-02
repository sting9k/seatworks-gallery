# Seatworks templates

The gallery of templates for [Seatworks](https://github.com/sting9k/seatworks), a Paseo plugin that runs a team of
coding agents. A template is a way of working: the roles of a team, what each one reads, and what is asked of the
team's record. You pick one, open it as a graph, change it, and install it. Nothing here is code.

**The gallery's page: https://sting9k.github.io/seatworks-gallery/**

## Use a template

1. Open [the gallery's page](https://sting9k.github.io/seatworks-gallery/), pick a template, and press **Open**. It
   opens as a graph you can change.
2. **Export** gives you one file, `<name>.template.json`.
3. In Paseo, open Seatworks' **Plugin** page, **Install a template**, and give the path of that file. The page says
   what the template brings before anything is installed: its roles, the agent profiles it names, each outside tool
   server it would run. Then install it, and attach a project with it.

A template steers agents that ask no leave for what they run. Read what one brings before you install it.

## Publish a template

A template is published by a pull request that adds its directory under `templates/`.

1. **Make it** in the editor, or by hand from Seatworks' `docs/TEMPLATE-SPEC.md`, which an agent can write one from.
2. **Check it** from a checkout of Seatworks:

   ```sh
   npm run template -- check <its directory>
   ```

   It says whether the template loads, the name it installs under, and what it needs of a machine.

3. **Name its directory as it installs.** The name in its `template.json`, in lower case with a dash for whatever is
   neither letter nor digit: `Night Crew` is kept in `templates/night-crew/`.
4. **Open a pull request.** The gallery is built on it. A template that does not load, or whose directory is not the
   name it installs under, fails the build, which says why. What the check only notes stops nothing.
5. **A reviewer reads it**: its prompts, its skills, and with most care any outside tool server it declares, since
   that is a command or an address every agent given it will reach.

Changing a template already here is a pull request too: it is a directory of text, so what changed reads line by line.

SLP, the template that comes with Seatworks, is listed from Seatworks' own repository and is not kept here. A
directory named `slp` here fails the build: a name is one template to install.

## How the page is built

`.github/workflows/gallery.yml` checks out this repository and Seatworks, builds the gallery from Seatworks' own
`templates/` and the `templates/` here, and builds Seatworks' editor beside it. On `main` the result is published to
this repository's GitHub Pages; on a pull request it is only built.

- Pages is switched on once, in this repository's settings: **Pages**, source **GitHub Actions**.
- The branch or tag of Seatworks it builds from is the repository variable `SEATWORKS_REF`, `main` when it is not set.
- The page follows Seatworks by itself. Every quarter of an hour `.github/workflows/seatworks-moved.yml` compares the
  commit the page was built from, which the page keeps at `built-from`, with where that branch is, and builds the page
  again when they differ. It starts one build for one commit: a build that failed is run again by hand, from
  **Actions**, **Gallery**, once what stopped it is mended.

To see the page on your own machine, with a checkout of Seatworks beside this one:

```sh
cd ../seatworks
npm ci
npm run gallery -- ../seatworks-gallery/templates
npx vite editor
```
