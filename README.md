# Awesome Autocomplete

At [Algolia](https://www.algolia.com), we're git *addicts* and love using GitHub to store every single idea or project we work on. We use it both for our private and public repositories ([12 API clients](https://www.algolia.com/doc/apiclients), [HN Search](https://github.com/algolia/hn-search) or various [d](https://github.com/algolia/instant-search-demo) [e](https://github.com/algolia/facebook-search) [m](https://github.com/algolia/linkedin-search) [o](https://github.com/algolia/meetup-search) [s](https://github.com/algolia/twitter-search)).

When you work on a instant-search engine all day long, not having relevant results after a few letters in a searchbar starts making you crazy. Chrome's [Omnibox](https://support.google.com/chrome/answer/95440) works pretty well but at the end navigation in a website should not be your browser's responsibility... So we did an [Algolia-powered Chrome extension](https://chrome.google.com/webstore/detail/chrome-awesome-autocomple/djkfdjpoelphhdclfjhnffmnlnoknfnd) :)

### Installation

Install it from [Chrome Web Store](https://chrome.google.com/webstore/detail/chrome-awesome-autocomple/djkfdjpoelphhdclfjhnffmnlnoknfnd).

### Features

Basically this Chrome extension replaces GitHub's searchbar and add auto-completion capabilities on:

 * top 1M public repositories
 * last 1M active users
 * your private repositories (for now, this one is done without Algolia, the list of private repositories stays in local)

![capture](capture.png)

## Development

### Installation

```sh
$ git clone https://github.com/algolia/chrome-awesome-autocomplete.git

# in case you don't have Grunt yet
$ sudo npm install -g grunt-cli
```

### Build instructions

```sh
$ cd chrome-awesome-autocomplete

# install dependencies
$ npm install

# generate your private key
$ openssl genrsa 2048 | openssl pkcs8 -topk8 -nocrypt > mykey.pem

# build it
$ grunt
```

When developing, write unit-tests, use `test-cont` Grunt task to check that your JS code passes linting tests and unit-tests.

When ready to try out the extension in the browser, use default Grunt task to build it. In `build` directory you'll find develop version of the extension in `unpacked-dev` subdirectory (with source maps), and production (uglified) version in `unpacked-prod` directory. The `.crx` packed version is created from `unpacked-prod` sources.

### Grunt tasks

* `clean`: clean `build` directory
* `test`: JS-lint and mocha test, single run
* `test-cont`: continuos `test` loop
* default: `clean`, `test`, build step (copy all necessary files to `build`
  directory, browserify JS sources, prepare production version (using uglify),
  pack the `crx` (using official shell script), and copy the resulting `crx` to
  CircleCI artifacts directory (only when on CircleCI))

