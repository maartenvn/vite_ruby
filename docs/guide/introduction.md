[library]: https://github.com/ElMassimo/vite_ruby
[vite_rails]: https://github.com/ElMassimo/vite_ruby/tree/main/vite_rails
[vite_hanami]: https://github.com/ElMassimo/vite_ruby/tree/main/vite_hanami
[plugin]: https://github.com/ElMassimo/vite_ruby/tree/main/vite-plugin-ruby
[vite]: https://vitejs.dev/
[webpacker]: https://github.com/rails/webpacker
[webpack]: https://github.com/webpack/webpack
[entrypoints]: /guide/development.html#entrypoints-⤵%EF%B8%8F
[deployment]: /guide/deployment
[rake tasks]: /guide/deployment.html#rake-tasks-⚙%EF%B8%8F
[recompile assets]: /guide/development.html#auto-build-🤖
[tag helpers]: /guide/rails.html#tag-helpers-🏷
[vite_rails]: https://github.com/ElMassimo/vite_ruby/tree/main/vite_rails
[vite_ruby]: https://github.com/ElMassimo/vite_ruby/tree/main/vite_ruby
[vite_hanami]: https://github.com/ElMassimo/vite_ruby/tree/main/vite_hanami
[no bundling]: https://vitejs.dev/guide/introduction.html#the-problem
[bundling]: https://vitejs.dev/guide/introduction.html#why-bundle-for-production

# Introduction

[__Vite Ruby__][library] is an umbrella project that library that provides full [Vite.js][vite] integration in Ruby web apps.

- <kbd>[vite_rails]</kbd> provides similar functionality as [webpacker] does for [webpack], without all the configuration overhead and dependencies.

- <kbd>[vite_hanami]</kbd> gets Vite up and running in Hanami web apps, including samples and tag helpers.

- <kbd>[vite_ruby]</kbd> can be used in plain Rack apps, and is all you need when using HTML entrypoints.


## Why Vite? 🤔

Vite [does not bundle your code during development][no bundling], which means the
dev server is extremely __fast to start__, and your changes will be __updated instantly__.

In production, Vite [bundles your code][bundling]
with tree-shaking, lazy-loading, and common chunk splitting out of the box, to achieve optimal loading performance.

Check [this video comparison with webpack](https://github.com/ElMassimo/pingcrm-vite/pull/1)
which demonstrates the difference in speed during development.

## Why Vite Ruby? 🤔

[Vite] is great on its own, but configuring it correctly to work for a Ruby app structure requires knowledge of its internals.

By following existing Rails and Rack conventions, and adding [a few of its own][plugin], it becomes possible for everyone to leverage [Vite] and its wonderful features!

## Features ⚡️

[Everything Vite provides](https://vitejs.dev/guide/features.html), plus:

#### 🤖 Automatic entrypoint detection

  Simply place your code under [`app/frontend/entrypoints`][entrypoints], and the [entrypoints]
  will be configured automatically.

#### ⚡️ Lightning-fast hot reload

  Because it does not bundle your code in development, only the scripts and styles that are running need to be processed, which enables Vite to have significantly faster HMR than webpack.

#### 🚀 Integrated with <kbd>assets:precompile</kbd>

  [Rake tasks] for building and cleaning Vite assets are [automatically integrated][deployment]
  with <kbd>assets:precompile</kbd> and <kbd>assets:clean</kbd>, so deploying is straightforward.

#### 🏗 Auto-build when not running Vite

  When the development server is not running, it will automatically detect
  changes and [recompile assets] for you. Makes it seamless to run integration tests.

#### 🏷 Smart tag helpers

  [Tag helpers] for <kbd>script</kbd> and <kbd>link</kbd> tags are provided, and
  will automatically output `preload` tags in production to optimize load time.
