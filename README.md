### ✏️ &nbsp; The Blog

I'm maintaining my blog at **[milos.marinkovic.xyz](https://milos.marinkovic.xyz)** in this repository.

It's built with [Jekyll](https://jekyllrb.com) and deployed directly after each change through [Vercel](https://vercel.com).

If you've found something incorrect (and want to address it), please open an issue or a PR.

### 🛠️ &nbsp; How to run locally

The full tutorial is [here](https://milos.marinkovic.xyz/2022/12/10/Jekyll-blogs-are-still-relevant).

In short… you'll need `ruby` and a couple of Ruby gems to run this. Google "how to install ruby" for your operating system to get the most recent installation instructions. MacOS should have it pre-installed.

Once that's done, install Jekyll:

```console
$ gem install jekyll
```

Then install Bundler:

```console
$ gem install bundler
```

And finally, run the bundler installation from the `Gemfile`:

```console
$ bundler install
```

Once done, you can simply run the `run.sh` script contained in this directory:

```console
$ ./run.sh
```
