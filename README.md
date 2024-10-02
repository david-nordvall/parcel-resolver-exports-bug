# `parcel-resolver-exports-bug`
This is a reproduction of a bug(?) in the `@parcel/resolver-default` package, where resolving exports in packages using objects in the `exports` property of their `package.json`. As an example in this reproduction, the package [`svelte-frech-toast`](https://svelte-french-toast.vercel.app/) is used.

Note: I'm calling this a "bug" here, but I realize that this is, in all likelyhood, a configuration error on my part 😄.

## How to use this?
For ease of use, this repo is configured to be opened as a [devcontainer](https://containers.dev/) with, for example, [Visual Studio Code](https://code.visualstudio.com/). In addition to an editor with devcontainer support, this requires that [Docker](https://www.docker.com/) is installed on your machine. If you have that, simply open this repo as a devcontainer and you should be good to go! If you have [Codespaces](https://github.com/features/codespaces) enabled on your Github account, you should be able to open this repo in a Codespace, directly from this repo's Github page, as well.

If you do not which to install Docker, etc. you should be able to use this repo as long as you have [Node](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) installed.

Once you have this repo set up you should be able to run the following to reproduce the bug(?):

```sh
> yarn install # This is already done if you use the devcontainer.
> yarn serve # Tries to serves up the reproduction on http://localhost:1234.
> yarn build # Tries to build a minified version of the reproduction.
```

Both `yarn serve` and `yarn build` will fail with the following error:

```
@parcel/resolver-default: Module 'svelte-french-toast' is not exported from the 'svelte-french-toast' package

  /workspaces/parcel-resolver-exports-bug/node_modules/svelte-french-toast/package.json:18:14
    17 |   "type": "module",
  > 18 |   "exports": {
  >    |              ^
  > 19 |     ".": {
  >    | ^^^^^^^^^^
  > 20 |       "types": "./dist/index.d.ts",
  >    | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  > 21 |       "svelte": "./dist/index.js"
  >    | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  > 22 |     }
  >    | ^^^^^
  > 23 |   },
  >    | ^^^
    24 |   "svelte": "./dist/index.js",
    25 |   "types": "./dist/index.d.ts",
```

My understanding from [Parcel's documentation](https://parceljs.org/features/dependency-resolution/#package-exports) is that adding the following snippet to my `package.json` would enable support for _exactly these types of exports_, but maybe I'm mistaken?

```json
{
  "@parcel/resolver-default": {
    "packageExports": true
  }
}
```